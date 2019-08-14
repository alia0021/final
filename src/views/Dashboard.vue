<template>
  <div>
    <h1>Dashboard</h1>
    <p>Welcome to your dashboard {{ user.name }}</p>
    <p>Your login email is: {{ user.email }}</p>
    <form @submit.prevent="submitForm">
      <label for="name">Edit your name:</label>
      <input type="text" id="name" v-model="user.name" />
      <br />
      <label for="age">Edit your age:</label>
      <input type="text" id="age" v-model="user.age" />
      <br />
      <label for="city">Edit your city:</label>
      <input type="text" id="city" v-model="user.city" />
      <br />
      <label for="job">Edit your job:</label>
      <input type="text" id="job" v-model="user.job" />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters({
      userData: "getUser"
    }),
    user() {
      return !this.userData ? false : this.userData;
    }
  },
  created() {
    this.getUserData();
  },
  methods: {
    ...mapActions(["updateUser", "fetchUser"]),
    submitForm() {
      const formData = {
        name: this.name,
        age: this.age,
        city: this.city,
        job: this.job
      };
      this.updateUser();
    },
    getUserData() {
      let userEmail = localStorage.getItem("userEmail");
      this.fetchUser(userEmail);
    }
  }
};
</script>
