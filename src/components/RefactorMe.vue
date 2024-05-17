<script setup lang="ts">
// TODO FIXME
export type State = '<' | '>'

export type StateValue = {
  a: State
  b: State
}

export type ListItem = {
  name: string
  level?: number
  state: StateValue
  exclude?: string[]
}

const DEFAULT_LEVEL = 10

defineProps<ListItem>()

const emit = defineEmits(['toggleState'])
</script>

<template>
  <!-- TODO FIXME -->
  <div class="vlock">
    <pre>name: {{ name }}</pre>
    <div>
      <button
        @click="
          () => {
            emit('toggleState', name, 'a')
          }
        "
      >
        A {{ state.a }}
      </button>
      &nbsp;
      <span
        v-for="(a, idx) of Array.from(Array(level ?? DEFAULT_LEVEL).keys())"
        :key="idx"
        >{{ a }},
      </span>
    </div>
    <div>
      <button
        @click="
          () => {
            emit('toggleState', name, 'b')
          }
        "
      >
        B {{ state.b }}
      </button>
      &nbsp;
      <span
        v-for="(b, idx) of Array.from(Array(level ?? DEFAULT_LEVEL).keys())"
        :key="idx"
        >{{ b }},
      </span>
    </div>
  </div>
</template>

<style>
.vlock {
  width: 80%;
  outline: 1px dashed var(--color-text);
}
</style>
