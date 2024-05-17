<script setup lang="ts">
import { ref } from 'vue'

const CHUNK_SIZE = 10
const list = ref<Array<Array<string>>>([])

function generateList() {
  list.value = []
  const length = Math.round(Math.random() * 100)

  const items = Array.from(Array(length).keys()).map((a) => a.toString())

  for (let index = 0; index < length; index += CHUNK_SIZE) {
    list.value.push(items.slice(index, index + CHUNK_SIZE))
  }
}
</script>

<template>
  <main>
    <pre>
      /**
      * Есть список неопределённой длинны от 1 до 100, необходимо отрисовать его уместив на этот экран.
      *
      * Например, если элементов 10 и они умещаются на экран, отобразить их как вертикальный список.
      * Если элементов 20, и они не умещаются одним списком, расположить их 2 списками в две колонки.
      * Если элементов 30, 3 столбца по 10 строк и т.д.
      *
      * П.С. Множитель 10 для примера, в одной колонке может быть как больше так и меньше элементов.
      * П.С. Размер самих элементов мы считаем фиксированным.
      */
    </pre>

    <button @click="() => generateList()">Сгенерировать список</button>

    <div class="list-wrapper">
      <!-- TODO -->

      <div v-for="(chunk, idx) of list" :key="idx" class="list-chunk">
        <div v-for="(item, idxc) of chunk" :key="idxc" class="list-item">
          {{ item }}
        </div>
      </div>

      <!-- TODO -->
    </div>
  </main>
</template>

<style scoped>
.list-wrapper {
  /* TODO */
  display: flex;

  gap: 1em;
  overflow: auto;
}

.list-chunk {
  display: flex;
  flex-direction: column;
}

.list-item {
  border: 1px solid var(--color-border);
  border-radius: 0.5em;
  background-color: var(--color-background-mute);

  width: 6ch;
  height: 2em;

  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
