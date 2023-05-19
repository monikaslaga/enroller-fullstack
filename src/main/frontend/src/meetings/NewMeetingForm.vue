<template>
  <form @submit.prevent="addNewMeeting()">
    <h3>Dodaj nowe spotkanie</h3>
    <label>Nazwa</label>
    <input type="text" v-model="newMeeting.title">
    <label>Opis</label>
    <textarea v-model="newMeeting.description"></textarea>
    <button>Dodaj</button>
    <span class="error" v-if="error">Spotkanie musi mieć nazwę!</span>
  </form>
</template>

<script>
export default {
  data() {
    return {
      newMeeting: {participants: []},
      error: false
    };
  },
  methods: {
    addNewMeeting() {
      var today = new Date();
      var dd = String(today.getDate()).padStart(2, '0');
      var mm = String(today.getMonth() + 1).padStart(2, '0');
      var yyyy = today.getFullYear();
      today = yyyy + '-' + mm + '-' + dd;

      this.newMeeting.date = today;

      this.error = false;
      if (this.newMeeting.title) {
        this.$emit('added', this.newMeeting);
        console.log('newMeeting added: ' + this.newMeeting);
      } else {
        this.error = true;
      }
    }
  }
}
</script>

<style scoped>
.error {
  padding-left: 30px;
  text-align: center;
  color: #F00;
}
</style>
