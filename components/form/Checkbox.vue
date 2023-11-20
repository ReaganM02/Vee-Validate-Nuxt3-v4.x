<script lang="ts" setup>
interface Props {
  value: boolean
  name: string
}

const { name, value } = defineProps<Props>()

// Vee validate
const { handleChange } = useField(name, undefined, {
  type: 'checkbox',
  checkedValue: value
})

</script>
<template>
  <div>
    <input
      :id="name"
      type="checkbox"
      :value="value"
      :name="name"
      @click="handleChange(value)"
    >
    <label
      :for="name"
      class="text-zinc-600 cursor-pointer select-none"
    >
      <slot />
    </label>
  </div>
</template>
<style scoped lang="css"></style>
