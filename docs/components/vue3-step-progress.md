# StepProgress

`StepProgress` is a an step progress bar component. Here's how to use it...

<template>
  <vue3-step-progress :steps="steps" :active-step="currentStep" />
</template>

Where steps are the list of labels to be displayed for each step and currentStep is the currently active step.

<code>
const steps = [
    "Step 1",
    "Step 2",
    "Step 3"
]
const currentStep = ref(1)
</code>

currentStep `1` indicates that the current active step is `Step 1`