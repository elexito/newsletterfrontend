<template>
  <div id="app">
    <!-- <form @submit.prevent="subscribe()">
      <input type="text" v-model="email" required="" />
      <input type="submit" value="Send Newsletter" required="" />
    </form> -->

    <div class="intro-header">
      <div class="container" align="center">
        <div class="tab-content custom-tab-content" align="center">
          <div class="subscribe-panel">
            <h1>Newsletter!!!</h1>
            <p>Subscribe to our weekly Newsletter and stay tuned.</p>

            <form @submit.prevent="subscribe()">
              <div class="col-md-4"></div>
              <div class="col-md-4">
                <div class="input-group">
                  <span class="input-group-addon"
                    ><i
                      class="glyphicon glyphicon-envelope"
                      aria-hidden="true"
                    ></i
                  ></span>
                  <input
                    type="text"
                    v-model="email"
                    class="form-control input-lg"
                    name="email"
                    id="email"
                    placeholder="Enter your Email"
                  />
                </div>
              </div>
              <div class="col-md-4"></div>
              <br /><br /><br />
              <button class="btn btn-warning btn-lg">Subscribe Now!</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

  data() {
    return {
      email: "",
    };
  },

  methods: {
    subscribe() {
      axios
        .post("http://localhost:8000/api/subscribe", { email: this.email })
        .then((response) => {
          console.log(response);
          this.$swal.fire("", response.data.message, "success");
        })
        .catch((err) => {
          const error = JSON.parse(JSON.stringify(err.response.data));
          console.log(error.errors.email);
          this.$swal.fire("", error.errors.email[0], "error");
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
