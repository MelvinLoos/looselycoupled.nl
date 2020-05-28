<template>
  <div>
    <!-- Masthead-->
    <header class="masthead">
      <div class="container d-flex h-100 align-items-center">
        <div class="mx-auto text-center">
          <h1 class="mx-auto my-0 text-uppercase">Loosely Coupled</h1>
          <h2
            class="text-white-50 mx-auto mt-2 mb-5"
          >Building applications, integrations and automations</h2>
          <!-- <a class="btn btn-primary js-scroll-trigger" href="#about">Get Started</a> -->
        </div>
      </div>
    </header>
    <section class="contact-section bg-black">
      <div class="container">
        <div class="row">
          <div class="col-md-10 col-lg-4 mx-auto text-center">
            <h2 class="text-white-60 mx-auto mt-2 mb-5" id="contact">Contact Us</h2>
            <form
              name="contact"
              method="post"
              v-on:submit.prevent="handleSubmit"
              action="/success/"
              data-netlify="true"
              data-netlify-honeypot="bot-field"
              class="form"
            >
              <input type="hidden" name="form-name" value="contact" />
              <p hidden>
                <label>
                  Don’t fill this out:
                  <input name="bot-field" />
                </label>
              </p>
              <div class="sender-info">
                <div>
                  <label for="name" class="label text-white-60">Your name</label>
                  <input type="text" name="name" v-model="formData.name" class="form-control w" />
                </div>
                <div>
                  <label for="email" class="label text-white-60">Your email</label>
                  <input type="email" name="email" v-model="formData.email" class="form-control" />
                </div>
              </div>

              <div class="message-wrapper">
                <label for="message" class="label text-white-60">Message</label>
                <textarea name="message" v-model="formData.message" class="form-control"></textarea>
              </div>

              <button type="submit" class="btn btn-primary mx-auto mt-4">Submit form</button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  metaInfo: {
    title: "Loosely Coupled - software development & consultancy"
  },
  data() {
    return {
      formData: {},
    }
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(key => encodeURIComponent(key) + '=' + encodeURIComponent(data[key]))
        .join('&')
    },
    handleSubmit(e) {
      fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({
          'form-name': e.target.getAttribute('name'),
          ...this.formData,
        }),
      })
      .then(() => this.$router.push('/success'))
      .catch(error => alert(error))
    }
  }
};
</script>

<style>
</style>
