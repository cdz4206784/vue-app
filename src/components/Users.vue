<template>
  <div class="users">
    <h1>Users</h1>
    <!-- 添加用户信息 -->
    <form action="" v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="Enter name">
      <input type="text" v-model="newUser.email" placeholder="Enter email">
      <input type="submit" value="Submit">
    </form>

    <!-- 展示用户信息 -->
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span v-bind:class="{contacted:user.contacted}">
           {{user.name}} : {{user.email}}
        </span>
        <button v-on:click="deleteUser(user)">x</button>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',

    data(){
      return {
        newUser: {},
        users: [
          {name:'Hemiah Wu',email:'hemiah@gmail.com',contacted:false},
          {name:'Henry Wu',email:'henry@gmail.com',contacted:false},
          {name:'Emily Wu',email:'emily@gmail.com',contacted:false}
        ]
      }
    },
    methods: {
      addUser(e){
        // console.log('hello');
        e.preventDefault();
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        })

      },
      deleteUser(user){
        // console.log("hello")
        this.users.splice(this.users.indexOf(user),1);
      }
    },
    created(){
      // console.log("Hello World!!!")
      this.$http.get("http://jsonplaceholder.typicode.com/users").then(res=>{
        // console.log(res.data)
        this.users = res.data
      })
    }
  }
</script>

<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>
