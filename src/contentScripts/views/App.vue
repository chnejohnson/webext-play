<script setup lang="ts">
import { useToggle } from '@vueuse/core'
import 'uno.css'

const [show, toggle] = useToggle(false)

const content = ref('')

onMounted(() => {
  // document.addEventListener('focus', handleFocusEvent, true)
  // document.addEventListener('blur', handleBlurEvent, true)
  document.addEventListener('input', handleInputEvent, true)
  document.addEventListener('mouseup', handleMouseUpEvent)
})

function handleInputEvent(event: Event) {
  const target = event.target
  if (target instanceof HTMLInputElement || target instanceof HTMLTextAreaElement)
    content.value = target.value
}

function handleMouseUpEvent() {
  if (window) {
    const selectedText = window.getSelection()?.toString()
    if (selectedText)
      content.value = selectedText
  }
}
</script>

<template>
  <div class="fixed right-0 bottom-0 m-5 z-100 flex flex-col items-end font-sans select-none leading-1em">
    <div
      class="bg-white text-gray-800 rounded-lg shadow h-[500px] w-[200px]"
      p="x-4 y-2"
      m="y-auto b-2"
      transition="opacity duration-300"
      :class="show ? 'opacity-100' : 'opacity-0'"
    >
      <h1 class="text-lg">
        Translator
      </h1>
      <p>{{ content }}</p>
    </div>
    <button
      class="flex w-10 h-10 rounded-full shadow cursor-pointer border-none"
      bg="teal-600 hover:teal-700"
      @click="toggle()"
    >
      <pixelarticons-power class="block m-auto text-white text-lg" />
    </button>
  </div>
</template>
