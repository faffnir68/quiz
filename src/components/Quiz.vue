<script lang="ts" setup>
import { onMounted, reactive, ref } from "vue"
import Progress from './Progress.vue'
import Question from './Question.vue'
import Button from "./Button.vue"
import Result from "./Result.vue"

let currentPage = ref(0)
let score = ref(0)

function nextPage() {
    if(currentPage.value >= 4) return
    currentPage.value++
}
</script>

<template>
    <div class="quiz">
        <div class="wrapper">
            <h1>Questionnaire sur les films et les series</h1>
            Score :{{ score }}
            <p>Page :{{ currentPage }}</p>
            <div v-if="currentPage < 4">
                <Progress :status="currentPage" />
                <Question v-model:score="score" v-model:currentPage="currentPage"  />
                <Button v-if="currentPage < 4" @click="nextPage()" />
            </div>
            <div v-if="currentPage == 4">
                <Progress :status="currentPage" />
                <Result :score="score" />
            </div>
        </div>
    </div>
</template>

<style>
    .quiz {
        padding: 20px;
        background-color: #f9f9f9;
        width: 1280px;
        height: 600px;
        color: #333;
    }
    .wrapper {
        margin: 0 auto;
        padding: 20px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }
    h1 {
        text-align: center;
        margin-bottom: 20px;
        font-size: 18px;
    }
</style>