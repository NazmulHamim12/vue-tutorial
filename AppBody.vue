<template>
  <div>
    <h1>Fetching with Python API</h1>

    <form @submit.prevent="formhandle">
      <label>First name:</label>
      <input type="text" v-model="form.f_name" />
      <hr />

      <label>Last name:</label>
      <input type="text" v-model="form.l_name" />
      <hr />

      <button type="submit">Click</button>
    </form>

    <!-- response দেখানোর জন্য -->
    <div v-if="response">
      <h3>Response from API:</h3>
      <pre>{{ response }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "http://127.0.0.1:5000/api/input",
      form: {
        f_name: "",
        l_name: ""
      },
      response: null
    };
  },
  methods: {
    async formhandle() {
      
        let formData = new FormData();
        formData.append("f_name", this.form.f_name);
        formData.append("l_name", this.form.l_name);

        let res = await fetch(this.url, {
          method: "POST",
          body: formData
        });

        this.response = await res.json();
        console.log(this.response)
      
    }
  }
};
</script>
