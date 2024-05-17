<script setup lang="ts">
import RefactorMe, {
  type ListItem,
  type State,
  type StateValue
} from '@/components/RefactorMe.vue'
import { reactive } from 'vue'

/* 

  Разделил отвественность между дочерним элементом и родительским. 
  т.к. родительский содержит набор данных для дочерних элементов, 
  то зона ответственности изменения этих данных так же должна ложиться на родительском элементе.

  Зона ответственности дочернего элемента - отображение и запуск событий на изменение.

*/

const list = reactive<ListItem[]>([
  {
    name: 'First',
    level: 5,
    state: {
      a: '>',
      b: '>'
    }
  },
  {
    name: 'Second',
    state: {
      a: '>',
      b: '>'
    },
    exclude: ['xqy', 'pon', 'sxr']
  }
])

function toggleState(itemName: ListItem['name'], state: keyof StateValue) {
  const toggle = (state: State) => {
    return state === '>' ? '<' : '>'
  }

  list.forEach((element) => {
    if (element.name === itemName) {
      if (state === 'a') {
        element.state.a = toggle(element.state.a)
      } else {
        element.state.b = toggle(element.state.b)
      }
    }
  })
}
</script>

<template>
  <main>
    <pre>
      /**
      * Необходимо отрефакторить компоненты `RefactorView.vue` и `RefactorMe.vue`
      */
    </pre>
    <!-- TODO FIXME -->
    <refactor-me
      :name="list[0].name"
      :level="list[0].level"
      :state="list[0].state"
      @toggleState="toggleState"
    />
    <refactor-me v-bind="list[1]" @toggleState="toggleState" />
  </main>
</template>

<style scoped></style>
