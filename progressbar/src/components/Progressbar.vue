<template>
  <div class="progressbar" :style="progressbarStyles" :class="isVerticalClass">
    <div
      class="step"
      :class="isVerticalClass"
      v-for="step in steps"
      :key="step.title"
      :style="isFullDuration(step)"
    >
      <div
        v-if="vertical"
        class="progression"
        :class="isVerticalClass"
        :style="{ height: stepProgressWidth(step) + '%' }"
      ></div>
      <div
        v-else
        class="progression"
        :class="isVerticalClass"
        :style="{ width: stepProgressWidth(step) + '%' }"
      ></div>

      <div
        v-if="step.checkpoint && step.checkpoint.has"
        class="checkpoint"
        :class="[isVerticalClass, checkpointStatus(step)]"
      >
      </div>
      <span v-if="isLongDuration(step)" class="step-progress-indicator">{{
        stepProgressWidth(step) + "%"
      }}</span>

      <v-tooltip activator="parent" location="top">{{ step.title }}</v-tooltip>
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
  height: 50%;
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
  border-top: 2px solid #fff;
  border-right: 1px solid #fff;
  border-bottom: 2px solid #fff;
  border-left: 1px solid #fff;
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
  font-size: 0.9em;
}

.step.vertical:nth-child(even) > .step-progress-indicator {
  transform: translateX(100%);
}

.step.vertical:nth-child(odd) > .step-progress-indicator {
  transform: translateX(-100%);
}

.checkpoint {
  position: absolute;
  border: 2px solid #fff;
  border-radius: 100%;
  aspect-ratio: 1/1;
  z-index: 10;
  background-size: 70%;
  background-position: center;
  background-repeat: no-repeat;
}

.checkpoint.done {
  background-color: #008000;
  background-image: url("../../src/assets/check.png");
}

.checkpoint.not-done {
  background-color: #fff;
}

.checkpoint.incomplete {
  background-color: #f73a3a;
  background-image: url("../../src/assets/close.png");
}

.checkpoint.vertical {
  width: 200%;
  top: 0;
  transform: translateY(-52%);
}

.checkpoint.horizontal {
  height: 200%;
  left: 0;
  transform: translateX(-52%);
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
    steps: {
      type: Object,
      required: true
    },
    vertical: {
      type: Boolean,
      required: false,
      default: false
    },
    width: {
      type: String,
      required: false,
      default: "100%"
    }
  },
  setup() {},
  data() {
    return {};
  },
  mounted() {},

  computed: {
    progressbarStyles() {
      return {
        width: `${this.height}`,
      };
    },
    isVerticalClass: function () {
      return this.vertical ? "vertical" : "horizontal";
    },
  },

  methods: {
    checkpointStatus(step) {
      if (step.checkpoint != null) {
        var start = new Date(step.date);
        var today = new Date();
        var end = new Date(start);
        end.setDate(end.getDate() + step.duration);

        if (start < today || step.checkpoint.done) {
          return step.checkpoint.done ? "done" : "incomplete";
        } else {
          return "not-done";
        }
      }
    },

    isFullDuration(step) {
      return this.vertical
        ? { height: this.isLongDuration(step) ? "100%" : "0%" }
        : { width: this.isLongDuration(step) ? "100%" : "0%" };
    },

    // isFullDuration(step) {
    //   return this.isLongDuration(step);
    // },

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

    isStepPassed(step) {
      var start = new Date(step.date);
      var today = new Date();
      // var end = new Date(start);
      // end.setDate(end.getDate() + step.duration);
      return today > start;
    },
  },
};
</script>