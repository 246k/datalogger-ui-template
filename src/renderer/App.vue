<script lang="ts" setup>
import Latest from './components/Latest.vue';
</script>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      port: '',
      response: [],
      errorMessage: '',
      endpoint: ''
    }
  },
  methods: {
    sendRequest() {
      // if(this.port){
        // fetch("https://localhost:" + this.port + '/getLatestValue/all')
        if(this.endpoint){
          fetch(this.endpoint)
            .then(async response => {
              const data = await response.json();

              if (!response.ok) {
                const error = (data && data.message) || response.statusText;
                return Promise.reject(error);
              }

              this.response = data;
            })
            .catch(error => {
              this.errorMessage = error;
              console.error("There was an error!", error);
            });
      }
    }
  },

  components: {
    Latest
  },
})
</script>


<template>
  <div id="app">
    <h1>Get Response</h1>
    <input v-model="endpoint" placeholder="Enter Endpoint" />
    <input id="sendButton" type="submit" value="Send Request" @click="sendRequest()">
    <div v-if="response">
      <h2>Response:</h2>
      <p>{{ response }}</p>
    </div>
    <!-- <Latest /> -->
  </div>
</template>
