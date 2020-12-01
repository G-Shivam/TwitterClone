<template>
  <div class="user-profile">
      <div class="user-profile__userpanel">
          <h1 class="user-profile__username">@{{user.username}}</h1>
          <div class="user-profile__admin-badge" v-if="user.isAdmin">
              Admin
          </div>
          <div class="user-profile__follower-count">
              <strong>Followers : </strong> {{followers}}
          </div>
          <Createtwitterpanel @add-tweet="addtweet"/>
      </div> 

      <div class="user-profile__tweets-wrapper">
            <Tweetitem v-for="tweet in user.tweets" :key="tweet.id" :username="user.username" :tweet="tweet"/>
      </div>
  </div>
</template>


<script>
import Tweetitem from "./Tweetitem";
import Createtwitterpanel from "./Createtwitterpanel";

export default {
  name: 'UserProfile',
  components: {Createtwitterpanel,Tweetitem},
  data(){
      return{
      followers : 0,
      user: {
        id: 1,
        username: 'be_my_amigo',
        FirstName: 'Shivam',
        LastName: 'Gupta',
        email: 'shivam5gupta52@gmail.com',
        isAdmin: true,
        tweets: [{
            id: 1, content:"This is Amazing"},
           { id: 2, content:"Going to Learn Much More"}
        ]

      }
    }},
   

  methods: {
    addtweet(tweet) {
         this.user.tweets.unshift ({
              id:  this.user.tweets.length + 1,
              content: tweet
         });
        }
    }
  
}
</script>

<style scoped>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-gap: 50px;
    padding: 50px 5%;
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3EB;

}
.user-profile__admin-badge{
    background: purple;
    color :white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1{
    margin: 0;
}

.user-profile__tweets-Wrapper{
    display: grid;
    grid-gap: 10px;

}

.user-profile__createtweet{
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}
.--exceeded{
    color: red;
    border-color: red;
    
}
.button{
    padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
}
</style>