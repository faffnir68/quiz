<script lang="ts" setup>
import { onMounted, reactive, ref, defineModel, watch } from "vue";

interface Question {
    question: string;
    choices: string[];
    correct_answer: string;
}

const quizData = reactive({
    quizData: []
})

const score = defineModel<number>('score')
const currentPage = defineModel<number>('currentPage')
let showAnswer = ref(false);

function checkAnswer(isCorrect: boolean) {
    showAnswer.value = true;
    if(isCorrect) {
        score.value = score.value+1;
    }
    disableInputs();
}

function disableInputs() {
    const inputs = document.querySelectorAll('input[type="radio"]');
    inputs.forEach(input => {
        (input as HTMLInputElement).disabled = true;
    });
}

watch(currentPage, () => {
    showAnswer.value = false
    const inputs = document.querySelectorAll('input[type="radio"]');
    inputs.forEach(input => {
        (input as HTMLInputElement).disabled = false;
        (input as HTMLInputElement).checked = false;
    });
})

onMounted( async () => {
    try {
        const response = await fetch('./quiz.json')
        if(!response.ok) {
            throw new Error('Loading file error')
        }
        const data = await response.json()
        quizData.quizData = data.questions
        console.log('Données du quiz chargées :', quizData)
    }
    catch (error) {
        console.log('Fetch error' + error)
    }
})

</script>

<template>
    <div v-for="(el, index) in quizData.quizData" :key="index">
    <div v-if="index === currentPage">
        <p>{{ el.question }}</p>
        <div>
            <div v-for="choice in el.choices" :key="choice">
                <input type="radio" name="choices" id="" value="{{ choice }}" @click.once="checkAnswer(choice === el.correct_answer)" />
                <label for="">{{ choice }}</label>
            </div>
        </div>
        <div class="answer" v-if="showAnswer">La bonne reponse etait : {{ el.correct_answer }}</div>
    </div>
</div>
</template>