<template>
  <div class="container shadow py-5 my-5">
    <h1 class="text-center my-3 display-4 italic font-weight-bold">
      <em>Cuenta regresiva</em>
    </h1>
    <div class="text-center my-5 py-4">
      <button v-on:click="run(3)" type="button" class="btn btn-outline-dark mx-4 my-4">3s</button>
      <button v-on:click="run(60)" type="button" class="btn btn-outline-dark mx-4 my-4">1m</button>
      <button v-on:click="run(300)" type="button" class="btn btn-outline-dark mx-4 my-4">5m</button>
      <button v-on:click="run(600)" type="button" class="btn btn-outline-dark mx-4 my-4">10m</button>
      <button v-on:click="run(1800)" type="button" class="btn btn-outline-dark mx-4 my-4">30m</button>
      <h1 class="display-2 text-center my-5">{{time}}seg/min</h1>
    </div>
  </div>
</template>

<script>
var interval;
export default {
  name: "HelloVue",
  data() {
    return {
      time: "00:00",
    };
  },
  methods: {
    run: function (seg) {
      clearInterval(interval);
      const now = Date.now();
      const end = now + (seg + 1) * 1000;
      this.descontar(end);
    },

    descontar: function (end) {
      interval = setInterval(() => {
        const resto = Math.round((end - Date.now()) / 1000);
        if (resto < 0) {
          clearInterval(interval);
          return;
        }
        const minutes = Math.floor((resto % 3600) / 60);
        const seconds = resto % 60;
        console.log(minutes, seconds);

        if (String(seconds).length === 1 && String(minutes).length === 1) {
          this.time = `0${minutes}:0${seconds}`;
        } else if (
          String(seconds).length === 1 &&
          String(minutes).length != 1
        ) {
          this.time = `${minutes}:0${seconds}`;
        } else if (
          String(seconds).length != 1 &&
          String(minutes).length === 1
        ) {
          this.time = `0${minutes}:${seconds}`;
        } else {
          this.time = `${minutes}:${seconds}`;
        }
      }, 1000);
    },
  },
};
</script>

<style scoped>


</style>
