<template>
  <q-btn :icon="icon" :title="t('defaults.copy')" @click.prevent.stop="copy" />
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import { writeToClipboard } from '../../helpers/clipboard'
  import { useTranslation } from '../../composables/i18n'

  const t = useTranslation()
  const props = defineProps<{ value?: string, customHandler?: any }>()

  const icon = ref('content_copy')
  const copy = () => {
    if (!props.value) return
    icon.value = 'done'

    if (props.customHandler) {
      props.customHandler.call()
    } else {
      writeToClipboard(props.value)
    }
    setTimeout(() => {
      icon.value = 'content_copy'
    }, 1000)
  }
</script>
