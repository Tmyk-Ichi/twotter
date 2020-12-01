<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile_username"> @{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
            <div class="user-profile__admin-badge" v-else>Not Admin</div>
        <div class="user-profile__follower-count">
            <strong>Follows:</strong>{{followers}}
        </div>
        </div>
        <div class="user-profile__twoots-wrapper">
        <TwootItem
        v-for='twoot in user.twoots'
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favorite='toggleFavorite'/>
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem';

export default {
    name:'UserProfile',
    components:{TwootItem},
     data(){
    return {
      followers: 0,
      user:{
        id:1,
        username:'_TomoyukiIchikawa',
        firstname:'Tomoyuki',
        lastname:'Ichikawa',
        email:'tmyk.ichikawa@gmail.com',
        isAdmin:false,
        twoots:[
            {id:1,content:'Twotter is amazing'},
            {id:2,content:'I can do it'},
        ]
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
    },
    toggleFavorite(id){
        console.log(`Favorited Tweet #${id}`);
    }
  },
  mounted(){
    this.followUser();
  }
  }

</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns:1fr 3fr;
    grid-gap:50px;
    padding:50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding:20px;
    background-color:white;
    border-radius: 5px;
    border:1px solid #DFE3E8;
}

.user-profile__admin-badge{
    background-color:purple;
    color: white;
    border-radius:5px;
    margin-right: auto;
    padding:0 10px;
    font-weight: bold;
}

h1{
    margin:0;
}
</style>
