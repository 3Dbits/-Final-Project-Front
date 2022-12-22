<script>
import {ErrorMessage, Field, Form} from "vee-validate";
import * as yup from "yup";
import Profile from "@/components/Profile.vue";

export default {
  name: "Register",
  components: {
    Profile,
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      username: yup
          .string()
          .required("Username is required!")
          .min(3, "Must be at least 3 characters!")
          .max(20, "Must be maximum 20 characters!"),
      email: yup
          .string()
          .required("Email is required!")
          .email("Email is invalid!")
          .max(50, "Must be maximum 50 characters!"),
      password: yup
          .string()
          .required("Password is required!")
          .matches(/^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}$/, "Password should have min 8 chars, one upercase/lowercase/number"),
      firstName: yup
          .string()
          .required("First name is required!")
          .min(2, "Must be at least 2 characters!")
          .max(40, "Must be maximum 40 characters!"),
      lastName: yup
          .string()
          .required("Last name is required!")
          .min(2, "Must be at least 2 characters!")
          .max(40, "Must be maximum 40 characters!"),
      dateOfBirth: yup
          .date()
          .required("Date of birth is required!")
    });

    return {
      successful: false,
      loading: false,
      message: "",
      schema,
      isHovering1: false,
      isHovering2: false,
      isHovering3: false,
      isHovering4: false,
      isHovering5: false,
      isHovering6: false,
      isHovering7: false,
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  mounted() {
    if (this.loggedIn) {
      this.$router.push("/userInfo");
    }
  },
  methods: {
    handleRegister(user) {
      this.message = "";
      this.successful = false;
      this.loading = true;

      this.$store.dispatch("auth/register", user).then(
          (data) => {
            this.message = data.message;
            this.successful = true;
            this.loading = false;
          },
          (error) => {
            this.message =
                (error.response &&
                    error.response.data &&
                    error.response.data.message) ||
                error.message ||
                error.toString();
            this.successful = false;
            this.loading = false;
          }
      );
    },
  },
};
</script>

<template>

  <section class="section">
    <Form :validation-schema="schema" class="box" @submit="handleRegister">

      <div class="field">
        <div v-if="message && message !== 'User registered successfully!'" class="notification is-danger" role="alert">
          <button class="delete" @click='message = ""'></button>
          {{ message }}
        </div>
      </div>

      <div class="field">
        <div v-if="message === 'User registered successfully!'" class="notification is-primary" role="alert">
          <button class="delete" @click='message = ""'></button>
          {{ message }}
        </div>
      </div>

      <div v-if="!successful">
        <div class="field">
          <label class="label" for="username">Username</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering1 = false"
             @mouseover="isHovering1 = true">
            <Field class="input is-rounded" name="username" placeholder="IvanHorvatić" type="text"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering1" icon="fa-solid fa-user-graduate"/>
            <font-awesome-icon v-if="isHovering1" beat icon="fa-solid fa-user-graduate"/>
            </span>
          </p>
          <ErrorMessage name="username"/>
        </div>

        <div class="field">
          <label class="label" for="email">Email</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering2 = false"
             @mouseover="isHovering2 = true">
            <Field class="input is-rounded" name="email" placeholder="IvanHorvatić@t.ht.hr" type="email"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering2" icon="fa-solid fa-envelope"/>
            <font-awesome-icon v-if="isHovering2" beat icon="fa-solid fa-envelope"/>
            </span>
          </p>
          <ErrorMessage name="email"/>
        </div>

        <div class="field">
          <label class="label" for="password">Password</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering3 = false"
             @mouseover="isHovering3 = true">
            <Field class="input is-rounded" name="password" placeholder="●●●●●●●●●●" type="password"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering3" icon="fa-solid fa-lock"/>
            <font-awesome-icon v-if="isHovering3" beat icon="fa-solid fa-lock"/>
            </span>
          </p>
          <ErrorMessage name="password"/>
        </div>

        <div class="field">
          <label class="label" for="firstName">First Name</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering4 = false"
             @mouseover="isHovering4 = true">
            <Field class="input is-rounded" name="firstName" placeholder="Ivan" type="text"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering4" icon="fa-solid fa-user-tag"/>
            <font-awesome-icon v-if="isHovering4" beat icon="fa-solid fa-user-tag"/>
            </span>
          </p>
          <ErrorMessage name="firstName"/>
        </div>

        <div class="field">
          <label class="label" for="lastName">Last Name</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering5 = false"
             @mouseover="isHovering5 = true">
            <Field class="input is-rounded" name="lastName" placeholder="Horvatić" type="text"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering5" icon="fa-solid fa-user-tag"/>
            <font-awesome-icon v-if="isHovering5" beat icon="fa-solid fa-user-tag"/>
            </span>
          </p>
          <ErrorMessage name="lastName"/>
        </div>

        <div class="field">
          <label class="label" for="dateOfBirth">Date of birth</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering6 = false"
             @mouseover="isHovering6 = true">
            <Field class="input is-rounded" name="dateOfBirth" placeholder="" type="date"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering6" icon="fa-solid fa-calendar-days"/>
            <font-awesome-icon v-if="isHovering6" beat icon="fa-solid fa-calendar-days"/>
            </span>
          </p>
          <ErrorMessage name="dateOfBirth"/>
        </div>

        <div class="field">
          <label class="label" for="bookId">Isbn of favorite book</label>
          <p class="control has-icons-left has-icons-right" @mouseout="isHovering7 = false"
             @mouseover="isHovering7 = true">
            <Field class="input is-rounded" name="bookId" placeholder="1234567891" type="number"/>
            <span class="icon is-small is-left">
            <font-awesome-icon v-if="!isHovering7" icon="fa-solid fa-book-open-reader"/>
            <font-awesome-icon v-if="isHovering7" beat icon="fa-solid fa-book-open-reader"/>
            </span>
          </p>
          <ErrorMessage name="bookId"/>
        </div>

        <p>
          <button :disabled="loading" class="button is-primary is-rounded">
            <span
                v-show="loading"
            ></span>
            <span>Sign Up</span>
          </button>
        </p>

        <p style="text-align: center">
          Already on BookLike?
          <router-link to="/login">Log in!</router-link>
        </p>

      </div>
    </Form>
  </section>

</template>

<style scoped>
.box {
  max-width: 33%;
  margin: auto;
}

@media screen and (max-width: 1200px) {
  .box {
    max-width: 50%;
    margin: auto;
  }
}
</style>
