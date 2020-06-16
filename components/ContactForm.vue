<template>
  <v-form
    ref="form"
    @submit.prevent="submitForm"
    v-model="valid"
    name="contact"
    data-netlify="true"
    data-netlify-honeypot="bot-field"
    method="POST"
    class="px-3 pb-4 text-center contact-form"
    lazy-validation
  >
    <input type="hidden" name="bot-field">
    <v-text-field
      v-model="name"
      :counter="20"
      :rules="nameRules"
      label="Name"
      required
      autofocus
      aria-placeholder="Your name is required"
    />

    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="E-mail"
      required
    />

    <v-select
      ref="request"
      v-model="request"
      :items="items"
      :rules="[v => !!v || 'Please make a selection']"
      label="Subject"
      required
      aria-placeholder="Please make a selection"
    />

    <v-textarea
      v-model="message"
      name="message"
      label="Message"
      rows="3"
    />

    <div class="text-center">
      <v-btn
        @click="reset"
        color="error"
        class="mr-4"
      >
        Reset
      </v-btn>
      <v-btn
        :disabled="!valid"
        @click.prevent="submitForm"
        color="success"
        class="mr-4"
      >
        Submit
      </v-btn>
    </div>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'Your name is required',
      v => (v && v.length <= 20) || 'Name must be less than 20 characters'
    ],
    email: '',
    emailRules: [
      v => !!v || 'Please enter your e-mail',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
    ],
    request: null,
    items: [
      'This site sux',
      'A new Vue.js webapp',
      'A new static website',
      'Add a feature ',
      'I have a question',
      'I have a problem'
    ],
    message: ''
  }),

  methods: {
    encode (data) {
      return Object.keys(data)
        .map(key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
        .join('/')
    },
    submitForm () {
      this.$refs.form.validate()
      if (this.$refs.form.hasError) {

      } else {
        this.handleSubmit()
      }
    },
    handleSubmit () {
      fetch('/', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        },
        body: this.encode({
          'form-name': 'contact',
          name: this.name,
          email: this.email,
          // phone: this.phone,
          request: this.request.toString(),
          message: this.message
        })
      })
    },
    reset () {
      this.$refs.form.reset()
    }
  }
}
</script>

<style scoped>
.contact-form {
  width: 90%;
}
</style>
