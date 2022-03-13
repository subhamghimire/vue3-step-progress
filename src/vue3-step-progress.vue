<template>
  <div class="step_progress_main">
    <div class="container">
      <ul id="progressbar">
        <li
          v-for="(step, index) in steps"
          :key="'step_' + index"
          :class="
            activeStep == index + 1 ? 'active' : '' + isCompleted(index + 1)
          "
        >
          {{ step }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, toRefs, watch, ref } from "vue";

export default defineComponent({
  props: {
    steps: {
      type: Array,
      required: true,
    },
    activeStep: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    const { activeStep } = toRefs(props);

    const oldStep = ref(1);

    watch(activeStep, (currentIndex, oldIndex) => {
      oldStep.value = oldIndex;
    });

    function isCompleted(index) {
      if (
        (activeStep.value > oldStep.value && index < activeStep.value) ||
        (index < activeStep.value && oldStep.value > index)
      )
        return "completed";
      return "";
    }
    return {
      isCompleted,
    };
  },
});
</script>
<style scoped>
ul {
  display: block;
  list-style-type: disc;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  padding-inline-start: 40px;
}
.step_progress_main {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.container {
  width: 100%;
  z-index: 1;
  margin: 0 auto;
}
#progressbar {
  counter-reset: step;
  width: 100% !important;
}
#progressbar li {
  position: relative;
  list-style: none;
  float: left;
  width: 33%;
  text-align: center;
  min-height: 10px;
  color: #707070;
}
#progressbar li:before {
  content: counter(step);
  counter-increment: step;
  width: 30px;
  height: 30px;
  border: 1px solid #c6c6c6;
  display: block;
  margin: 0 auto 10px auto;
  border-radius: 50%;
  line-height: 25px;
  background: #c6c6c6;
  color: #707070;
  text-align: center;
  font-weight: bold;
  margin-bottom: -4rem;
  position: relative;
  z-index: 9;
}
#progressbar li:after {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  background: #e3e3e3;
  top: 15px;
  left: -50%;
  z-index: -1;
}
#progressbar li.active {
  color: #045cab;
}

#progressbar li.active:before,
#progressbar li.completed:before {
  background: #045cab;
  color: white;
  border: 1px solid #045cab;
}

#progressbar li.completed:before {
  content: "✔";
}

#progressbar li.active:after,
#progressbar li.completed:after {
  background: #045cab;
}

#progressbar li:first-child:after {
  content: none;
}
</style>
