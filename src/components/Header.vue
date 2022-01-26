<template>
  <div>
    <v-app-bar color="#240046" dense dark>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-spacer></v-spacer>
      <v-toolbar-title>Challenge Vue + Vuetify</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text @click="logout">Log Out</v-btn>
    </v-app-bar>
  </div>
</template>
<script>
export default {
    name: "Header",
    data() {
        return {
        user: {
            username: "",
            password: "",
            error: false,
            error_msg: "",
        },
        };
    },
    methods: {
        logout() {
        localStorage.removeItem("challenge_token");
        this.$router.push("/");
        },
    },
}
</script>