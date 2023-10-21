<template>
  <div class="progressbar" :class="isVerticalClass">
    <div class="step" :class="isVerticalClass" v-for="step in steps" :key="step.title"
      :style="{ 'width': isLongDuration(step) ? '100%' : '0%' }">
      <div v-if="vertical" class="progression" :class="isVerticalClass" :style="{ height: stepProgressWidth(step) + '%' }"></div>
      <div v-else class="progression" :class="isVerticalClass" :style="{ width: stepProgressWidth(step) + '%' }"></div>
      <div v-if="step.checkpoint.has" class="checkpoint" :class="isVerticalClass"></div>
      <span class="step-progress-indicator">{{
        stepProgressWidth(step) + "%"
      }}</span>
    </div>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.progressbar {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.progressbar.vertical {
  flex-direction: column;
  height: 100%;
  width: 20px;
}

.progressbar.horizontal {
  flex-direction: row;
  max-height: 50px;
  height: 20px;
  min-height: 10px;
  width: 50%;
}

.step {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid #fff;
  background: #fff;
}

.step.vertical {
  width: 100%;
  height: 100%;
}

.step.horizontal {
  width: 100%;
  height: 100%;
}

.step.vertical:first-child {
  border-radius: 50px 50px 0 0;
}

.step.vertical:last-child {
  border-radius: 0 0 50px 50px;
}

.step.horizontal:first-child {
  border-radius: 50px 0 0 50px;
}

.step.horizontal:last-child {
  border-radius: 0 50px 50px 0;
}

.step-progress-indicator {
  position: absolute;
}

.step.vertical:nth-child(even) > .step-progress-indicator{
  transform: translateX(100%);
}

.step.vertical:nth-child(odd) > .step-progress-indicator{
  transform: translateX(-100%);
}

.checkpoint {
  position: absolute;
  border: 2px solid #fff;
  background: green;
  border-radius: 100%;
  aspect-ratio: 1/1;
  z-index: 10;
}

.checkpoint.vertical {
  width: 130%;
  top: 0;
  transform: translateY(-51%);
}

.checkpoint.horizontal {
  height: 130%;
  left: 0;
  transform: translateX(-51%);
}

.progression {
  position: absolute;
  background: greenyellow;
}

.progression.vertical {
  top: 0;
  width: 100%;
}

.progression.horizontal {
  left: 0;
  height: 100%;
}
</style>


<script>
export default {
  name: "Progress-bar",
  // props: ["steps", "vertical"],
  props: {
    steps: Object,
    vertical: Boolean
  },
  setup() {
    // console.log(props);
  },
  data() {
    return {
      // isVertical: this.vertical
    };
  },
  mounted() {
    console.log(this.vertical);
  },

  computed: {
    isVerticalClass: function () {
      return this.vertical ? 'vertical' : 'horizontal';
    }
  },
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
      // console.log(step.duration > 1);
      return step.duration > 1;
    },

  },
};
</script>