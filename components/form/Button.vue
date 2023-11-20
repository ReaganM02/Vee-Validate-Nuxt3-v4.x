<script lang="ts" setup>
interface Props {
  label: string
  loading?: boolean
  type?: 'button' | 'submit'
}
const { type = 'button' } = defineProps<Props>()
</script>
<template>
  <button
    :type="type"
    class="px-4 py-2 bg-blue-500 text-white rounded disabled:bg-blue-300 disabled:cursor-not-allowed disabled:opacity-50 relative overflow-hidden"
    :disabled="loading"
  >
    <span
      v-if="loading"
      class="absolute left-0 right-0 bottom-0 top-0 grid place-content-center bg-blue-500"
    >
      <IconLoading class="w-[18px]" />
    </span>
    <span>{{ label }}</span>
  </button>
</template>
<style scoped lang="css"></style>
