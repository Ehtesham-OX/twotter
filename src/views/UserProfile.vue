<template>
  <h1>@{{ user[0].userName }} ---- {{ fullName }}</h1>
  <h2>{{ userId }}</h2>
  <br />
  <strong>Followers: {{ followers }}</strong>
  <br />
  <button @click="incrementFollower">Be My Follower</button>
  <hr />
  <Twoots
    v-for="twoot in user[0].twoots"
    :key="twoot.id"
    :twoot="twoot"
    @clicked="showTwootClicked"
  />
  <hr />
  <form @submit.prevent="newTwoot" class="user-profile__form">
    <input type="text" placeholder="Say Title..." v-model="newTwootTitle" />
    <textarea
      :class="{ '--exceded': formExeded > 50 }"
      cols="30"
      rows="10"
      placeholder="Say Somthing..."
      v-model="newTwootContent"
    ></textarea>
    <button>Submit</button>
  </form>
</template>

<script>
import Twoots from "@/components/Twoots";
import { useRoute } from "vue-router";

export default {
  name: "UserProfile",
  components: {
    Twoots,
  },
  data() {
    return {
      followers: 0,
      newTwootTitle: "",
      newTwootContent: "",
      user: [
        {
          id: 1,
          userName: "Ehtesham-OX",
          firstName: "Ehtesham",
          lastName: "Zahraei",
          email: "ehtesham.ox@gmail.com",
          isAdmin: true,
          twoots: [
            {
              id: 1,
              title: "Che khabar?",
              content: "Hello Mammad!",
              isFavo: false,
            },
            { id: 2, title: "Khobi?", content: "Hello Asghar!", isFavo: false },
          ],
        },
        {
          id: 2,
          userName: "Mammad Zaharei",
          firstName: "Mammad",
          lastName: "Zahraei",
          email: "Zaharei.ox@gmail.com",
          isAdmin: true,
          twoots: [
            {
              id: 1,
              title: "Che khabar?",
              content: "Hello Mammad!",
              isFavo: false,
            },
            { id: 2, title: "Khobi?", content: "Hello Asghar!", isFavo: false },
          ],
        },
      ],
    };
  },
  watch: {
    followers(oldFollower, newFollower) {
      if (oldFollower !== newFollower)
        console.log(`${this.user.userName} has gained the follower!`);
    },
  },
  computed: {
    fullName() {
      return `${this.user[0].firstName} ${this.user[0].lastName}`;
    },
    formExeded() {
      return this.newTwootContent.length;
    },
    userId() {
      return useRoute().params.userid;
    },
  },
  methods: {
    incrementFollower() {
      this.followers++;
    },
    showTwootClicked(id) {
      this.user.twoots.forEach((twoot) => {
        if (twoot.id === id) twoot.isFavo = true;
        else twoot.isFavo = false;
      });
    },
    newTwoot() {
      this.user.twoots.push({
        id: this.user.twoots.length + 1,
        title: this.newTwootContent,
        content: this.newTwootContent,
        isFavo: false,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
strong {
  background-color: rosybrown;
}
form {
  --execeded {
    background-color: red;
  }
}
</style>
