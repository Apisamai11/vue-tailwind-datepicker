<script setup lang="ts">
import dayjs, { months } from 'dayjs'
import { ref, watch } from 'vue'
import type { Dayjs } from 'dayjs'
import VueTailwindDatePicker from './VueTailwindDatePicker.vue'

const dateValue = ref('2024-09-01')

const currentLocale = ref('th')
const locales = ['en', 'es', 'de', 'th']

const formatter = ref({
  date: 'YYYY-MM-DD',
  month: 'MMM',
  year: currentLocale.value == 'th' ? 'BBBB' : 'YYYY',
})

function onClickSomething(e: Dayjs) {
  console.log(e)
}

function onSelectSomething(e: Dayjs) {
  console.log(e)
}

watch(currentLocale, (val) => {
  formatter.value.year = currentLocale.value == 'th' ? 'BBBB' : 'YYYY'
})
</script>

<template>
  <div class="p-10 bg-sky-50 min-h-screen">
    <label>
      Choose one locale
      <select v-model="currentLocale" name="language" class="mb-6">
        <option v-for="locale in locales" :key="locale" :value="locale">
          {{ locale }}
        </option>
        >
      </select>
    </label>
    <div class="grid grid-rows-2 gap-4">
      <VueTailwindDatePicker
        v-model="dateValue"
        :isBuddhistEra="currentLocale == 'th' ? true : false"
        as-single
        :formatter="formatter"
        :i18n="currentLocale"
        @select-month="onSelectSomething($event)"
        @select-year="onSelectSomething($event)"
        @select-right-month="onSelectSomething($event)"
        @select-right-year="onSelectSomething($event)"
        @click-prev="onClickSomething($event)"
        @click-next="onClickSomething($event)"
        @click-right-prev="onClickSomething($event)"
        @click-right-next="onClickSomething($event)"
      />

      <!-- <VueTailwindDatePicker
        v-model="dateValue.startDate"
        as-single
        :i18n="currentLocale"
      /> -->
    </div>
  </div>
</template>
