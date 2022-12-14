<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";

export default {
  name: "Login",
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      username: yup.string().required("Username is required!"),
      password: yup.string().required("Password is required!"),
    });

    return {
      loading: false,
      message: "",
      schema,
      isHovering1: false,
      isHovering2: false
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  created() {
    if (this.loggedIn) {
      this.$router.push("/profile");
    }
  },
  methods: {
    handleLogin(user) {
      this.loading = true;

      this.$store.dispatch("auth/login", user).then(
          () => {
            this.$router.push("/profile");
          },
          (error) => {
            this.loading = false;
            this.message =
                (error.response &&
                    error.response.data &&
                    error.response.data.message) ||
                error.message ||
                error.toString();
            if (this.message === "Request failed with status code 401") {
              this.message = "Bad credentials!";
            }
          }
      );
    },
  },
};
</script>

<template>
      <Form @submit="handleLogin" :validation-schema="schema" class="box">

        <div class="field">
          <div class="notification is-danger" v-if="message" role="alert">
            <button class="delete" @click='message = ""'></button>
            {{ message }}
          </div>
        </div>

        <div class="field">
          <label for="username" class="label">Username</label>
          <p class="control has-icons-left has-icons-right" @mouseover="isHovering1 = true" @mouseout="isHovering1 = false">
            <Field name="username" type="text" class="input is-rounded" placeholder="IvanHorvatić"/>
            <span class="icon is-small is-left">
            <font-awesome-icon icon="fa-solid fa-user-graduate" v-if="!isHovering1"/>
            <font-awesome-icon icon="fa-solid fa-user-graduate" beat  v-if="isHovering1"/>
            </span>
          </p>
          <ErrorMessage name="username" style="color: red"/>
        </div>
          <div class="field">
          <label for="password" class="label">Password</label>
          <p class="control has-icons-left has-icons-right" @mouseover="isHovering2 = true" @mouseout="isHovering2 = false">
            <Field name="password" type="password" class="input is-rounded" placeholder="●●●●●●●●●●"/>
            <span class="icon is-small is-left">
            <font-awesome-icon icon="fa-solid fa-lock" v-if="!isHovering2"/>
            <font-awesome-icon icon="fa-solid fa-lock" beat v-if="isHovering2"/>
            </span>
          </p>
          <ErrorMessage name="password" style="color: red"/>
          </div>

          <p>
            <button :disabled="loading" class="button is-primary is-rounded">
            <span
                v-show="loading"
            ></span>
              <span>Login</span>
            </button>
          </p>
      </Form>
</template>

<style scoped>
  .box {
    max-width: 50%;
    margin: auto;
  }
</style>
