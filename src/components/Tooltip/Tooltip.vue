<template>
  <div class="vk-tooltip">
    <div class="vk-tooltip__trigger" ref="triggerNode" @click="tooglePopper">
      <slot />
    </div>
    <div v-if="isOpen" class="vk-tooltip__popper" ref="popperNode">
      <slot name="content">
        {{ content }}
      </slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { createPopper } from '@popperjs/core'
import type { Instance } from '@popperjs/core'
import type { TooltipProps, TooltipEmits } from './types'
const props = withDefaults(defineProps<TooltipProps>(), {
  placement: 'bottom'
})
const emits = defineEmits<TooltipEmits>()
const isOpen = ref(false)
const popperNode = ref<HTMLElement>()
const triggerNode = ref<HTMLElement>()
let popperInstance: null | Instance = null
const tooglePopper = () => {
  isOpen.value = !isOpen.value
  emits('visible-change', isOpen.value)
}
watch(isOpen, (newValue) => {
  if(newValue) {
    if(triggerNode.value && popperNode.value) {
      popperInstance = createPopper(triggerNode.value, popperNode.value, { placement: props.placement })
    } else {
      popperInstance?.destroy()
    }
  }
}, { flush: 'post' })
</script>