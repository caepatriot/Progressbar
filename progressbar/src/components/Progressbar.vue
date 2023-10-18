<template>
  <div class="progressbar">

    <div class="progression"></div>

    <div class="step" v-for="step in steps" :key="step.title">
      <div v-if="step.checkpoint.has" class="checkpoint"></div>
      <span class="step-progress-indicator">{{ step.title }}</span>
    </div>

  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.progressbar {
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  max-height: 50px;
  height: 20px;
  min-height: 10px;
  width: 50%;
}

.progression {
  position: absolute;
  background: greenyellow;
  height: 100%;
  width: 75%;
  left: 0;
  /* z-index: 5; */
}

.step {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid grey;
  /* background: green; */
  width: 100%;
  height: 100%;
}

.step-progress-indicator {}

.checkpoint {
  position: absolute;
  border: 2px solid #fff;
  background: green;
  height: 130%;
  /* width: 200%; */
  border-radius: 100%;
  left: 0;
  transform: translateX(-51%);
  aspect-ratio: 1/1;
  z-index: 10;
}
</style>


<script>
export default {
  name: 'Progress-bar',
  props: ['steps'],
  data() {
    return {

    }
  },
  mounted() {
    // this.steps = props.steps;
  },
}
</script>