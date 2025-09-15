<script lang="ts" setup>
interface Score {
    score: number;
}

defineProps<{
    score: Score,
}>()
</script>

<template>
  <div class="quiz">
        <h2>Quiz Termine!</h2>
        <p>Vos resultats vont s'afficher ici.</p>
        <p>{{ score }} points</p>
    </div>
</template> 