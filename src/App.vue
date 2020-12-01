<template>
  <div id="app">
    @{{user.username}} -- {{fullname}}
    <strong>follows:</strong>{{followers}}
    <button @click="followUser">follow</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      followers: 0,
      user:{
        id:1,
        username:'_TomoyukiIchikawa',
        firstname:'Tomoyuki',
        lastname:'Asano',
        email:'tmyk.ichikawa@gmail.com',
        isAdmin:'true',
      }
    }
  },
  watch:{
    followers(newFollowerCount,oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower`)
      }
    }
  },
  computed:{
    fullname(){
      return `${this.user.firstname} ${this.user.lastname}`
    }
  },
  methods:{
    followUser(){
      this.followers++
    }
  },
  mounted(){
    this.followUser();
  }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display:flex;
  flex-direction: column;
}
</style>
