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
      "App heruterladen",
      " QR Code scannen",
      "Google Authentictor aktivieren",
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
