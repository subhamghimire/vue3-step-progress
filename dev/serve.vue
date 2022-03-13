<script>
import { defineComponent, ref } from "vue";
import Vue3StepProgress from "@/vue3-step-progress.vue";

export default defineComponent({
  name: "ServeDev",
  components: {
    Vue3StepProgress,
  },
  setup() {
    const steps = [
      "Step 1",
      "Step 2",
      "Step 3",
    ];
    const currentStep = ref(1);
    return {
      steps,
      currentStep,
    };
  },
});
</script>

<template>
  <div id="app">
    <vue3-step-progress :steps="steps" :active-step="currentStep" />
  </div>
</template>
