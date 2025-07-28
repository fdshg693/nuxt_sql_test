<template>
  <div class="quiz">
    <h1>簡単な計算クイズ</h1>
    <p>{{ question }}</p>
    <input type="number" v-model.number="answer" @keyup.enter="check"/>
    <button @click="check">答え合わせ</button>
    <p v-if="result !== null">
      <span v-if="result">正解です！新しい問題を出します。</span>
      <span v-else>残念、不正解です。</span>
    </p>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const a = ref(0)
const b = ref(0)
const answer = ref<number|null>(null)
const result = ref<boolean|null>(null)

function newQuestion() {
  a.value = Math.floor(Math.random() * 10)
  b.value = Math.floor(Math.random() * 10)
  answer.value = null
  result.value = null
}

newQuestion()

const question = computed(() => `${a.value} + ${b.value} = ?`)

function check() {
  if (answer.value === a.value + b.value) {
    result.value = true
    newQuestion()
  } else {
    result.value = false
  }
}
</script>

<style scoped>
.quiz {
  max-width: 400px;
  margin: 2rem auto;
  text-align: center;
}
</style>
