<template>
  <Progressbar :steps="steps" />
</template>

<script>
import Progressbar from './components/Progressbar.vue';

export default {
  name: 'App',
  components: {
    Progressbar
},
  data() {
    return {
      steps: [
        {
          title: "step 1",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 1",
            done: true,
            has: true
          }
        },
        {
          title: "step 2",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 2",
            done: true,
            has: true
          }
        },
        {
          title: "step 3",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 3",
            done: true,
            has: true
          }
        },
        {
          title: "step 4",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 4",
            done: true,
            has: true
          }
        },
        {
          title: "step 5",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 5",
            done: true,
            has: true
          }
        },
        {
          title: "step 6",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 6",
            done: true,
            has: true
          }
        },
        {
          title: "step 7",
          date: new Date(),
          duration: 10,
          checkpoint: {
            title: "checkpoint 7",
            done: true,
            has: true
          }
        }
      ]
    }
  },
}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  height: 100vh;
  width: 100vw;
}
</style>
