<template>
  <section class="container posts-page">
    <span>new posts</span>
    <b-table striped
      :items="items"
    >
    </b-table>
  </section>
</template>

<script>
export default {
  data(){
    return {
      items: [
        // { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        // { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        // { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
        // { age: 38, first_name: 'Jami', last_name: 'Carney' }
        {
          id: '001',
          title: 'aa',
          body: 'aaaaaa',
          created_at: '2018/08/10 12:00:00',
          user: {
            id: 'testaa'
          }
        }
      ]
    }
  }
  // computed:{
  //   showPosts(){
  //     return [
  //       {
  //         id: '001',
  //         title: 'aa',
  //         body: 'aaaaaa',
  //         created_at: '2018/08/10 12:00:00',
  //         user: {
  //           id: 'testaa'
  //         }
  //       }
  //     ]
  //   }
  // }
}
</script>

