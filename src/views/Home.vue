<template>
  <div class="home">
    <div>
      <button @click="fetchXHR()">fetchXHR</button>
      <button @click="fetchPromise()">fetchPromise</button>
      <button @click="fetchAsyncAwait()">fetchAsyncAwait</button>
      <pre style="text-align:left">{{response}}</pre>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'home',
  data() {
    return {
      response: '',
    };
  },
  components: {
    // HelloWorld,
  },
  methods: {
    fetchXHR() {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', '/data.json');
      xhr.send();
      xhr.onload = (event) => {
        this.response = event.target.response;
      };
    },
    fetchPromise() {
      window.fetch('/data.json')
        .then(res => res.json())
        .then((res) => { this.response = JSON.stringify(res, undefined, 4); });
    },
    async fetchAsyncAwait() {
      const response = await window.fetch('/data.json');
      const json = await response.json();
      this.response = json;
    },
  },
};
</script>

<style lang="scss">
  button {
    padding: 10px;
    margin: 4px;
    font-size: 1em;
    cursor: pointer;
    font-weight: bold;
  }
</style>
