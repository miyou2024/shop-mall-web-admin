<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import { useAppStore } from './store'
import { naiveI18nOptions } from '@/utils'

const appStore = useAppStore()

const naiveLocale = computed(() => {
  return naiveI18nOptions[appStore.lang] ? naiveI18nOptions[appStore.lang] : naiveI18nOptions.enUS
})

const theme = computed(() => appStore.colorMode === 'dark' ? darkTheme : null)
</script>

<template>
  <n-config-provider
    class="wh-full" inline-theme-disabled :theme="theme"
    :locale="naiveLocale.locale" :date-locale="naiveLocale.dateLocale" :theme-overrides="appStore.theme"
  >
    <naive-provider>
      <router-view/>
      <Watermark :show-watermark="appStore.showWatermark" />
    </naive-provider>
  </n-config-provider>
</template>
