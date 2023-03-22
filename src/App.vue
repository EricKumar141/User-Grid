<template>

 <div>
  <v-app style="background-color: antiquewhite;">
      
        <UserList />
</v-app>
</div>

</template>

<script>
import UserList from './components/UserList.vue'
export default {
  name: 'App',
  data() {
      return {
        currUser: {},
        editMode: false, // prevents user from viewing another user card details when in edit mode
      };
    },

  components: {
    UserList,
  },
}
</script>

<style>
html { overflow-y: auto }
</style>

