<script setup lang="ts">
import { ref } from 'vue'
import TypeMe, { type SelectValue } from '@/components/TypeMe.vue'

// TODO FIXME

type RefElement = {
  innerState: number
}

type DefaultState = {
  state: RefElement['innerState']
}

const elementRef = ref<RefElement>({ innerState: 0 })

function select(key: string, value: SelectValue) {
  alert(`Select ${key} with type ${typeof value}`)
}

function hover(e: MouseEvent) {
  elementRef.value.innerState = e.x
}
</script>

<template>
  <main>
    <pre>
      /**
      * Необходимо типизировать компоненты `TypesView.vue` и `TypeMe.vue`
      */
    </pre>
    <type-me name="First" :options="new Map<string, SelectValue>()"></type-me>
    <type-me
      :options="
        new Map([
          ['key1', 1],
          ['key2', 0],
          ['key3', 4]
        ])
      "
      is-fun
      @select="select"
    ></type-me>
    <type-me
      ref="elementRef"
      :name="`X: ${elementRef.innerState}`"
      :options="
        new Map([
          ['key1', { a: 'a' }],
          ['key2', { a: 'b' }]
        ])
      "
      :is-fun="false"
      @select="select"
      @hover="hover"
    >
      <template #default="{ state }: DefaultState">
        <i>X: {{ state }}</i>
      </template>
    </type-me>
  </main>
</template>

<style scoped></style>
