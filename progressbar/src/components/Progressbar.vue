<template>
  <div class="progressbar">
    <div class="step" v-for="step in steps" :key="step.title">
      <div
        class="progression"
        :style="{ width: stepProgressWidth(step) + '%' }"
      ></div>
      <div v-if="step.checkpoint.has" class="checkpoint"></div>
      <span class="step-progress-indicator">{{
        stepProgressWidth(step) + "%"
      }}</span>
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
  left: 0;
}

.step {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid #fff;
  background: #fff;
  width: 100%;
  height: 100%;
}

.step:first-child {
  border-radius: 50px 0 0 50px;
}

.step:last-child {
  border-radius: 0 50px 50px 0;
}

.step-progress-indicator {
  position: absolute;
}

.checkpoint {
  position: absolute;
  border: 2px solid #fff;
  background: green;
  height: 130%;
  border-radius: 100%;
  left: 0;
  transform: translateX(-51%);
  aspect-ratio: 1/1;
  z-index: 10;
}

.checkpoint-done {
  background-image: url("../../assets/icons/check.png");
}

.checkpoint-not-done {
}
</style>


<script>
export default {
  name: "Progress-bar",
  props: ["steps"],
  data() {
    return {
    };
  },
  mounted() {},
  computed: {},
  methods: {
    stepProgressWidth(step) {
      var start = new Date(step.date);
      var today = new Date();
      var end = new Date(start);
      end.setDate(end.getDate() + step.duration);
      if (end < today) {
        return 100;
      } else if (today > start && today < end) {
        var progress = this.dateDiff(start, today);
        var goal = this.dateDiff(start, end);
        return Math.ceil((progress / goal) * 100);
      } else {
        return 0;
      }
    },
    dateDiff(startDate, endDate) {
      const date1 = new Date(startDate);
      const date2 = new Date(endDate);
      const diffTime = Math.abs(date2 - date1);
      const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
      return diffDays;
    },
    isLongDuration(step) {
      return step.duration > 1;
    },
  },
};
</script>