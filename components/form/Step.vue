<script lang="ts" setup>

const stepCounter = inject<Ref<number>>('STEP_COUNTER')!.value++
const currentStepIndex = inject<Ref<number>>('CURRENT_STEP_INDEX')

const showCurrentForm = computed(() => {
  return stepCounter === currentStepIndex!.value
})

</script>
<template>
  <div>
    <div v-if="showCurrentForm">
      <slot />
    </div>
  </div>
</template>
<style scoped lang="css"></style>
