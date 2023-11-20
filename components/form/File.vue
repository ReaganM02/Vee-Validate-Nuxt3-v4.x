<script lang="ts" setup>
interface Props {
  value?: string
  name: string
}

const { name, value } = defineProps<Props>()


// Ref Properties
const fileData = ref<File | null>(null)
const preview = ref<string | null>(null)

// Vee Validate
const { handleChange, setErrors, errorMessage, handleReset, meta } = useField(name, undefined, {
  initialValue: value
})

// Functions
function fileChange (event: Event) {
  const file = (event.target as HTMLInputElement).files![0]
  // If size is greater than 500kb
  if (file.size > 500000) {
    console.log('hit')
    setErrors('Maximum of 500kb only.')
    return
  }
  handleChange(event)
  fileData.value = file
  preview.value = URL.createObjectURL(file)
}

function removeFile () {
  handleReset()
  preview.value = null
}

// Life cycle hooks
onMounted(() => {
  handleReset()
})

</script>
<template>
  <div>
    <label
      :for="name"
      :class="{ 'error': !!errorMessage, 'success': meta.valid }"
    >
      <div
        class="p-2 bg-zinc-50 border-dashed border-2 border-zinc-200 rounded-md cursor-pointer text-zinc-500 hover:border-zinc-300 duration-200"
        title="Upload file"
      >
        <div
          v-if="fileData && preview"
          class="w-full flex gap-2"
        >
          <div>
            <img
              :src="preview"
              class="w-[50px] h-[50px]"
            />
            <span
              @click="removeFile"
              class="relative z-[10] text-sm"
              title="Remove file"
            >replace</span>
          </div>
          <div>
            <div>{{ fileData.name }}</div>
            <div class="text-sm opacity-60">{{ fileData.type }}</div>
          </div>
        </div>
        <div v-else>
          <div class="flex gap-2 items-center">
            <span class="bg-zinc-200 text-center rounded-md px-2 py-1 text-sm font-light text-zinc-500">
              Browse a file
            </span>
            <div class="text-sm mt-1">
              PNG, WEBP, JPG (MAX. 500KB)
            </div>
          </div>
        </div>
        <input
          type="file"
          :id="name"
          :name="name"
          @change="fileChange"
          class="hidden"
          accept="image/png, image/webp, image/jpg"
        />
      </div>
    </label>
    <div class="text-rose-500 text-sm mt-1">
      {{ errorMessage }}
    </div>
  </div>
</template>
<style scoped lang="css">
.error > div {
  @apply text-rose-600 border-rose-100 bg-rose-50;
}

.success > div {
  @apply text-green-500 bg-green-100 border-green-200;
}
</style>
