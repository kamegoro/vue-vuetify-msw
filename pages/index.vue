<template>
  <div>
    <h1>ユーザー 一覧</h1>
    <v-data-table
      :headers="headers"
      :items="state.users"
      :items-per-page="5"
      class="elevation-1"
    >
    </v-data-table>
  </div>
</template>

<script lang="ts">
import { 
  defineComponent,
  reactive,
  onMounted,
} from 'vue';

type User = {
  id: number
  name: string
}

type State = {
  users: User[]
}

export default defineComponent({
  name: 'IndexPage',

  async asyncData({ $axios }) {
    const headers = [
      { text: 'ID', value: 'id' },
      { text: '名前', value: 'name' },
    ];

    const state = reactive<State>({
      users: [],
    })

    try {
      const res = await $axios.get(`/users`);
      state.users = res.data;
      console.log(state.users)
    } catch (err) {
      console.log(err)
    }

    return { headers, state }
  }
})
</script>
