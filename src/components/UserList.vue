<template>
    <v-navigation-drawer clipped-left style = "width: 50%; display: inline-block;">
   <v-container grid-list-md
   color = "grey">
    <v-row no-gutters
    flex-row
    justify="center">
        <v-col 

        xs="12" 
        sm="5" 
        md="3"
        flex-col
        cols="2"
        class="align-center"
        v-for ="user in users">


        <v-card
        style="background-color: gainsboro; overflow: hidden;"
        variant="outlined"
        aspect = "1"
        color = "#546E7A"
        @click="selectUser(user)">

    <v-img
      :src="user.image"
      cover
      style="width:40%; background-color: lightsteelblue; margin-top: 1%; margin-left: 1%;border-radius: 100px;"
    ></v-img>

    <v-card-title 
    class="text-center" style="color:darkslategray;">
      {{user.firstName}} {{ user.lastName }}
    </v-card-title>
            </v-card>
            <v-spacer></v-spacer>
        </v-col>
    </v-row>
  </v-container>
</v-navigation-drawer>

<div class="right" v-if="userSelected">
      <UserCard :user="selectedUser" @editModeOn="toggleEditMode" />
    </div>
  </template>
  
<script>
  import UserCard from './UserCard.vue';
  export default {
    name: 'UserList',
    components: {
      UserCard,
    },
    data() {
      return {
        users: [],
        selectedUser: {},
        userSelected: false,
        editMode: false, // prevents user from viewing another user card details when in edit mode
      };
    },
    methods: {
      selectUser(user) {
        if (!this.editMode) {
          this.selectedUser = user;
          this.userSelected = true;
        }
      },
      toggleEditMode(data) {
        this.editMode = data;
      },
    },
    mounted() {
      fetch('https://dummyjson.com/users')
        .then((res) => res.json())
        .then((data) => (this.users = data.users))
        .catch((error) => console.log(error));
    },

  };
  </script>
  
  <style>
  </style>
  