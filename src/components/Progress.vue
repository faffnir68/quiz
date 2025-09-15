<script lang="ts" setup>
import { reactive, defineProps } from 'vue' 

interface Status {
    status: number;
}

defineProps<{
    status: Status,
}>()
</script>

<template>
    <div class="progress">
        <progress id="progressbar" max="4" :value="status"></progress>
    </div>
</template>

<style>
    progress {
    width: 320px;
    height: 14px;
    appearance: none;
    -webkit-appearance: none;
    border: none;
    background: none;
    }

    /* Fond de la barre */
    progress::-webkit-progress-bar {
    background: color-mix(in srgb, #000 6%, #fff); /* léger gris */
    border-radius: 999px;
    overflow: hidden; /* arrondis sur le fill */
    }

    /* Portion remplie (Chrome/Safari/Edge) */
    progress::-webkit-progress-value {
    background: linear-gradient(90deg, #6ee7b7, #3b82f6);
    border-radius: 999px;
    transition: width .35s ease;
    }

    /* Portion remplie (Firefox) */
    progress::-moz-progress-bar {
    background: linear-gradient(90deg, #6ee7b7, #3b82f6);
    border-radius: 999px;
    transition: width .35s ease;
    }

    /* Thème sombre (optionnel) */
    @media (prefers-color-scheme: dark) {
    progress::-webkit-progress-bar { background: #1f2937; }
    }
</style>