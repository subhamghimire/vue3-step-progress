<template>
  <div class="step_progress_main">
    <div class="container">
      <ul class="progressbar">
        <li
          v-for="(step, index) in steps"
          :key="'step_' + index"
          :class="activeStep == index + 1 ? 'active' : '' + isCompleted(index + 1)"
          class="progress__item"
        >
          {{ step }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { defineComponent, toRefs, watch, ref } from 'vue';

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
        return 'completed';
      return '';
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

@media only screen and (min-width: 768px) {
  .container {
    width: 100%;
  }
  .step_progress_main {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .progressbar {
    counter-reset: step;
    width: 100% !important;
  }
  .progress__item {
    position: relative;
    list-style: none;
    float: left;
    width: 33%;
    text-align: center;
    min-height: 10px;
    color: #707070;
  }
  .progress__item:before {
    content: counter(step);
    counter-increment: step;
    width: 30px;
    height: 30px;
    border: 1px solid #c6c6c6;
    display: block;
    margin: 0 auto 10px auto;
    border-radius: 50%;
    line-height: 30px;
    background: #c6c6c6;
    color: #707070;
    text-align: center;
    font-weight: bold;
    margin-bottom: -4rem;
    position: relative;
    z-index: 9;
  }
  .progress__item:after {
    content: '';
    position: absolute;
    width: 100%;
    height: 2px;
    background: #e3e3e3;
    top: 15px;
    left: -50%;
    z-index: -1;
  }
}

.progress__item.active {
  color: #045cab;
}

.progress__item.active:before,
.progress__item.completed:before {
  background: #045cab;
  color: white;
  border: 1px solid #045cab;
}

.progress__item.completed:before {
  content: '✔';
}

.progress__item.active:after,
.progress__item.completed:after {
  background: #045cab;
}

.progress__item:first-child:after {
  content: none;
}
@media only screen and (max-width: 768px) {
  .step_progress_main {
    display: flex;
    flex-direction: column;
  }

  .progressbar {
    counter-reset: step;
    position: relative;
  }
  .progress__item {
    position: relative;
    list-style: none;
    color: #707070;
    min-height: 100px;
  }
  .progress__item:before {
    content: counter(step);
    counter-increment: step;
    width: 30px;
    height: 30px;
    border: 1px solid #c6c6c6;
    display: block;
    margin: 20px auto 10px auto;
    border-radius: 50%;
    line-height: 30px;
    background: #c6c6c6;
    color: #707070;
    text-align: center;
    font-weight: bold;
    margin-bottom: -4rem;
    position: absolute;
    z-index: 9;
  }
  .progress__item:after {
    content: '';
    height: 35px;
    width: 1px;
    background: #e3e3e3;
    position: absolute;
    top: -35px;
    left: 1rem;
    border: none;
    z-index: -1;
  }
}
</style>
