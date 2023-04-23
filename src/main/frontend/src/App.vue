<template>
  <div id="app">
    <h1>Witaj w systemie do zapisów na zajęcia</h1>

    <div v-if="authenticatedUsername">
      <UserPanel :username="authenticatedUsername" @logout="logMeOut()"></UserPanel>
      <MeetingsPage :username="authenticatedUsername"></MeetingsPage>
    </div>
    <div v-else>
      <button @click="signingUp = false" :class="signingUp ? 'button-outline' : ''">Loguję się</button>
      <button @click="signingUp = true" :class="!signingUp ? 'button-outline' : ''">Rejestruję się</button>
      <div v-if="" class="alert">
        {{message}}
      </div>
      <LoginForm v-if="signingUp" @login="(user) => register(user)" button-label="Załóż konto"></LoginForm>
      <LoginForm v-else @login="(user) => logMeIn(user)"></LoginForm>
    </div>
  </div>
</template>

<script>
import "milligram";
import LoginForm from "./LoginForm";
import UserPanel from "./UserPanel";
import MeetingsPage from "./meetings/MeetingsPage";
import axios from "axios";

export default {
  components: {LoginForm, MeetingsPage, UserPanel},
  data() {
    return {
      message:'',
      signingUp: false,
      authenticatedUsername: '',
    }
  },
  methods: {
    logMeIn(user) {
      this.authenticatedUsername = user.login;
    },
    logMeOut() {

      this.authenticatedUsername = '';
    },
    register(user) {
      axios.post('api/participants', user)
          .then(response => {
this.message='Udało się założyć konto';
          })
          .catch(response => {
this.message= 'Nie udało się założyć konta';
          });
    }

  }
}
</script>

<style>
#app {
  max-width: 1000px;
  margin: 0 auto;
}
.alert {
  padding: 5px;
  margin: 30px;
  border: 2px solid green;
  background: lightblue;
  font-siza: 2 em;
}
</style>
