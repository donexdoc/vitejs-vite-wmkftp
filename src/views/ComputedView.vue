<script setup lang="ts">
import { computed, ref, watch } from 'vue'

type IStruct = Array<{ val: string; pos: number }>

// Исключительно для удобства заполнения данных в этом примере
const _strOriginal = ref('')
const exclideFilter = ref('')

// Оригинальный объект
const structOriginal = computed<IStruct>(() =>
  _strOriginal.value.split('').map((a, i) => ({ val: a, pos: i }))
)

// Финальный объект который получается после фильтрации
const structFinal = computed<IStruct>(() =>
  structOriginal.value.filter((a) => !exclideFilter.value.includes(a.val))
)

const countChanges = ref(0)

const changed = (newValue: IStruct, oldValue: IStruct) => {
  if (newValue.length !== oldValue.length) {
    return true
  }

  for (let index = 0; index < newValue.length; index++) {
    if (
      oldValue === undefined ||
      oldValue[index]?.pos !== newValue[index].pos ||
      oldValue[index]?.val !== newValue[index].val
    ) {
      return true
    }
  }

  return false
}

watch(
  () => structFinal.value,
  (newValue, oldValue) => {
    if (!changed(newValue, oldValue)) return

    countChanges.value += 1

    const parent = document.querySelector('#burnrow')
    const child = document.createTextNode('🔥')

    parent?.appendChild(child)
    setTimeout(() => parent?.removeChild(child), 1000)
  }
)
</script>

<template>
  <main>
    <pre>
      /**
      * Есть объект `structOriginal`, из него получается отфильтрованный объект `structFinal`
      * используя `letters4filtering` для этого.
      * 
      * На реактивное обновление `structFinal` завязана дополнительная js 
      * логика которая запускает "тяжёлые" функции, в примере 🔥 и счётчик.
      * 
      * Тип объектов и сама механика фильтрации не играет роли в этой задаче.
      *
      * Проблема: Для объекта `structFinal` черезмерно часто срабатывает реактивность, 
      * даже тогда как сам объект не изменился.
      *
      * Как можно решить эту проблему?
      *
      * П.С. Необходимо чтобы реактивность срабатывала только при изменении `structFinal`
      */
    </pre>
    <div>
      Letters:
      <input v-model="_strOriginal" />
    </div>
    <div>
      Exclude:
      <input v-model="exclideFilter" />
    </div>
    <div>
      Result:
      {{ structFinal.reduce((acc, a) => acc + a.val, '') }}
    </div>
    <div>Changes of result: {{ countChanges }}</div>
    <div id="burnrow">🤖</div>
  </main>
</template>
