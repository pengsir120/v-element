<template>
  <button
    class="vk-button"
    :class="{
      [`vk-button--${type}`]: type,
      [`vk-button--${size}`]: size,
      'is-plain': plain,
      'is-round': round,
      'is-circle': circle,
      'is-disabled': disabled
    }"
    :disabled="disabled"
  >
    <span>
      <slot />
    </span>
  </button>
</template>

<script setup lang="ts">
import type { ButtonProps } from './types'

defineOptions({
  name: 'VkButton'
})
defineProps<ButtonProps>()
</script>

<style scoped>
</style>