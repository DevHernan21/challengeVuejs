<template>
  <v-main class="fadeInDown">
    <v-card width="500" class="mx-auto mt-9" id="login-card">
      <div class="contentCard">
        <v-card-text>
          <v-img
            height="50%"
            width="50%"
            class="mx-auto fadeIn first"
            src="@/assets/LOGO1.png"
            id="icon"
          >
          </v-img>
          <form v-on:submit.prevent="login">
            
              <div class="containerForm fadeIn second">
                <v-text-field
                  color="#240046"
                  class="fadeIn second"
                  v-model="username"
                  :rules="usernameRules"
                  label="Username"
                  type="text"
                  prepend-icon="mdi-account-circle"
                  @keyup.native.enter="login"
                ></v-text-field>
                
                <v-text-field
                  color="#240046"
                  class="fadeIn third"
                  v-model="password"
                  :rules="passwordRules"
                  label="Password"
                  type="password"
                  prepend-icon="mdi-lock"
                  @keyup.native.enter="login"
                ></v-text-field>
              </div>
            
            <div>
              <v-btn
                class="fadeIn fourth btnLogin"
                type="submit"
              >
                Log in
              </v-btn>
            </div>
          </form>
        </v-card-text>
        <div>
          <v-alert
            border="bottom"
            color="btn-outline-purple"
            dark
            role="alert"
            v-if="error"
          >
            <v-icon>mdi-alert-circle</v-icon> {{ error_msg }}
          </v-alert>
        </div>
      </div>
    </v-card>
  </v-main>
</template>
<script>
import axios from "axios";

export default {
  name: "Login",
  components: {},
  data() {
    return {
      username: "",
      password: "",
      error: false,
      error_msg: "",
      usernameRules: [(v) => !!v || "Username is required"],
      passwordRules: [
        (v) => !!v || "Password is required",
        (v) => v.length >= 6 || "Password must be at least 6 characters",
      ],
    };
  },
  methods: {
    login() {
      let json = {
        username: this.username,
        password: this.password,
      };
      axios
        .post("http://vps.churrasco.digital:3005/login", json)
        .then((response) => {
          console.log(response);
          if (response.status == 200) {
            localStorage.setItem("challenge_token", response.data.token);
            this.$router.push("/products");
          }
        })
        .catch((error) => {
          this.error = true;
          this.error_msg = "Invalid username or password";
          console.log(error, "Login failed");
        });
    },
  },
  created() {},
};
</script>
<style scoped>
#icon {
  width: 60%;
}
#login-card {
  background-color: #1F132D;
  border-radius: 10px;
  box-shadow: 0px 0px 10px #1E269A;
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  text-align: center;
  padding: 30px;
  width: 90%;
  max-width: 450px;
  position: relative;
  padding: 0px;
  -webkit-box-shadow: 0 30px 60px 0 rgba(0, 0, 0, 0.3);
  box-shadow: 0 30px 60px 0 rgba(0, 0, 0, 0.3);
}
.fadeInDown {
  -webkit-animation-name: fadeInDown;
  animation-name: fadeInDown;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
@-webkit-keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}
@keyframes fadeInDown {
  0% {
    opacity: 0;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
  }
  100% {
    opacity: 1;
    -webkit-transform: none;
    transform: none;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.fadeIn {
  opacity: 0;
  -webkit-animation: fadeIn ease-in 1;
  -moz-animation: fadeIn ease-in 1;
  animation: fadeIn ease-in 1;
  -webkit-animation-fill-mode: forwards;
  -moz-animation-fill-mode: forwards;
  animation-fill-mode: forwards;
  -webkit-animation-duration: 1s;
  -moz-animation-duration: 1s;
  animation-duration: 1s;
}
.fadeIn.first {
  -webkit-animation-delay: 0.4s;
  -moz-animation-delay: 0.4s;
  animation-delay: 0.4s;
}
.fadeIn.second {
  -webkit-animation-delay: 0.6s;
  -moz-animation-delay: 0.6s;
  animation-delay: 0.6s;
}
.fadeIn.third {
  -webkit-animation-delay: 0.8s;
  -moz-animation-delay: 0.8s;
  animation-delay: 0.8s;
}
.fadeIn.fourth {
  -webkit-animation-delay: 1s;
  -moz-animation-delay: 1s;
  animation-delay: 1s;
}
.underlineHover:after {
  display: block;
  left: 0;
  bottom: -10px;
  width: 0;
  height: 2px;
  background-color: #56baed;
  content: "";
  transition: width 0.2s;
}
.underlineHover:hover {
  color: #0d0d0d;
}
.underlineHover:hover:after {
  width: 100%;
}
.containerForm {
  background: #ffffff;
  margin-top: 1rem;
  margin-bottom: 1rem;
  margin-right: 4rem;
  margin-left: 4rem;
  padding: 1rem;
  border-radius: 1rem;
}
.btnLogin {
  background: #540F95;
  color: #ffffff;
}
</style>