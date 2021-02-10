<template>
    @{{ user.userName }} ---- {{ fullName }}
    <br>
    <strong>Followers: {{ followers }}</strong>
    <br>
    <button @click="incrementFollower">Be My Follower</button>
    <hr>
    <Twoots v-for="twoot in user.twoots"
            :key="twoot.id" 
            :twoot="twoot"
            @clicked="showTwootClicked"
    />
    <hr>
    <form @submit.prevent="newTwoot">
        <input type="text" placeholder="Say Title..." v-model="newTwootTitle">
        <textarea cols="30" rows="10" placeholder="Say Somthing..." v-model="newTwootContent"></textarea>
        <button>Submit</button>
    </form>

</template>

<script>
import Twoots from './Twoots';

export default {
  name: 'UserProfile',
  components: {
        Twoots,
  },
  data () {
    return {
        followers: 0,
        newTwootTitle: '',
        newTwootContent: '',
        user: {
            userName: 'Ehtesham-OX',
            firstName: 'Ehtesham',
            lastName: 'Zahraei',
            email: 'ehtesham.ox@gmail.com',
            isAdmin: true,
            twoots: [
                { id:1, title:'Che khabar?', content:'Hello Mammad!', isFavo: false },
                { id:2, title:'Khobi?', content:'Hello Asghar!', isFavo: false },
            ]
        } 
    }
  },
  watch: {
    followers(oldFollower, newFollower) {
      if(oldFollower !== newFollower)
        console.log(`${this.user.userName} has gained the follower!`);
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    incrementFollower() {
        this.followers++;
    },
    showTwootClicked(id) {
        this.user.twoots.forEach(twoot => {
            if(twoot.id === id )
                twoot.isFavo = true;
            else 
                twoot.isFavo = false;
        });
    },
    newTwoot() {
        this.user.twoots.push({
            id: this.user.twoots.length + 1,
            title: this.newTwootContent,
            content: this.newTwootContent,
            isFavo: false
        });
    }
  },
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
}
</style>
