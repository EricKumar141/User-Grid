<template>
<v-card

style="float:right; width:45%; margin-top: 4%; color: lightsteelblue; margin-right: 2.5%; height: 900px; background-color: darkgrey;"
        variant="tonal"
    aspect = "1"
    color = "#546E7A"
    class="float: right; d-flex justify-center"
  >
  <v-img
      :src="user.image"
      cover
      style="position: absolute; top:50px; left:50px; width:250px; height:250px; background-color: lightsteelblue;
  justify-content: flex-start; margin-top:2%; margin-left: 2%; border-style: solid;"

    ></v-img>
    <div v-if="!editMode" >
        <v-card-title style = "position: absolute;
    display:block;
    top:400px;
    left:75px; color:darkslategray">
    Name: {{ user.firstName }} {{user.lastName}}</v-card-title>


    <v-card-title style = "position: absolute; 
    display:block;
    top:500px;
    left:75px; color:darkslategray;">
    Email: {{ user.email}}</v-card-title>
    </div>


    <div v-if="editMode">
    <v-form fast-fail @submit.prevent variant="outlined"  style = "position: absolute;
    display:block;
    top:400px;
    left:75px;
    width: 250px; color:darkslategray;">
      <v-text-field
        v-model="form.name"
        :rules="userNameRules"
        label="User Name"
      ></v-text-field>

      <v-text-field
        v-model="form.email"
        :rules="emailRules"
        label="Email"
      ></v-text-field>
      
    </v-form>
</div>
<v-button class="cancelBtn" v-if="editMode" @click="revertForm">Cancel</v-button>
<v-button class="saveBtn" v-if="editMode" @click="updateUser">Save</v-button>
    <v-button class = "editBtn" v-if="!editMode" @click="toggleEditMode">Edit</v-button>
    
    
    
            </v-card>

    
  </template>
  
  <script>
  export default {
    name: 'UserCard',
    data() {
      return {
        editMode: false,
        form: {
          name: this.user.firstName + ' ' + this.user.lastName,
          email: this.user.email,
        },
        userNameRules: [
        value => {
            const namePattern = /^[a-zA-Z]+ [a-zA-Z]+$/;
              if (this.form.name.length === 0 || !namePattern.test(this.form.name)) {
                this.errors.formUserName = false;
                return 'Invalid UserName'
        }
          else{
            this.errors.formUserName = true;
            return true
          }
          
        },
      ],
      emailRules: [
        value => {
            const emailPattern = /^[A-Za-z0-9_!#$%&'*+\/=?`{|}~^.-]+@[A-Za-z0-9.-]+$/
            if (this.form.email.length === 0 || !emailPattern.test(this.form.email)) {
                this.errors.formEmail = false;
                return 'Invalid email'
        }
          else{
            this.errors.formEmail = true;
            return true

          }
          
        },
      ],
        errors: {
            formUserName: true,
            formEmail: true,
        },
      };
    },
    props: {
      user: {},
    },
    methods: {
      toggleEditMode() {
        this.editMode = !this.editMode;
        this.$emit('editModeOn', this.editMode); // prevents parent from selecting another user when in edit mode
      },
      updateUser() {
        if(this.errors.formUserName && this.errors.formEmail){
        console.log('Updated User');
        console.log(this.form);
        this.toggleEditMode();
        }
      },
      revertForm() {
        // reset input fields
        this.form.name = this.user.firstName + ' ' + this.user.lastName;
        this.form.email = this.user.email;
        this.toggleEditMode();
      },
    },
  };
  </script>
  
  <style>
  v-button {
    background-color: rgb(28, 86, 194);
    color: white;
    border: none;
    text-align: center;
    font-size: 32px;
    height:60px;
    width: 144px;
    border-radius: 6px;
  }
  v-button.editBtn {
    position: absolute;
    bottom:0;
    margin-right: 2%;
    margin-bottom: 2%;
  }

  v-button.saveBtn {
    position:absolute;
    bottom:0;
    right:50px;
    margin-bottom: 2%;
  }
  
  v-button.cancelBtn {
    position: absolute;
    bottom:0;
    margin-bottom: 2%;
  }
  v-button:active {
    transform: translateY(+0.15em);
  }
  v-card-title{
    position: absolute;
    bottom:0;
    background-color:black;
  }

  </style>
  