<template>
  <Progressbar :steps="steps" />
</template>

<script>
import Progressbar from "./components/Progressbar.vue";

export default {
  name: "App",
  components: {
    Progressbar,
  },
  data() {
    return {
      steps: [
        {
          title: "step 1",
          date: new Date("01/18/2022"),
          duration: 100,
          checkpoint: {
            title: "checkpoint 1",
            done: true,
            has: true,
          },
        },
        {
          title: "step 2",
          date: new Date("04/22/2022"),
          duration: 30,
          checkpoint: {
            title: "checkpoint 2",
            done: true,
            has: true,
          },
        },
        {
          title: "step 3",
          date: new Date("05/22/2022"),
          duration: 20,
          checkpoint: {
            title: "checkpoint 3",
            done: true,
            has: false,
          },
        },
        {
          title: "step 4",
          date: new Date("06/11/2022"),
          duration: 100,
          checkpoint: {
            title: "checkpoint 4",
            done: true,
            has: true,
          },
        },
        {
          title: "step 5",
          date: new Date("09/19/2022"),
          duration: 50,
          checkpoint: {
            title: "checkpoint 5",
            done: true,
            has: true,
          },
        },
        {
          title: "step 6",
          date: new Date("10/14/2023"),
          duration: 10,
          checkpoint: {
            title: "checkpoint 6",
            done: true,
            has: true,
          },
        },
        {
          title: "step 7",
          date: new Date("12/12/2023"),
          duration: 100,
          checkpoint: {
            title: "checkpoint 7",
            done: true,
            has: true,
          },
        },
      ],
    };
  },
  mounted() {},
  computed: {},
  methods: {},
};
</script>

<style>
body {
  margin: 0;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  background: red;
}
</style>
