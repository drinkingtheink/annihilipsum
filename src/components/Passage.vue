<template>
    <div class="the-passage">
        <p>
            <span 
                v-for="word, index in passageInWords" 
                :key="word" 
                class="word"
                v-bind:style="{ animationDelay: index + '00ms' }"
            >
                {{ word }}
            </span>
        </p>
    </div>
</template>

<script>
export default {
    name: 'Passage',
    props: {
        passage: String,
        passageInWords: Array
    },
    methods: {
        genAniDelay() {
            return `0.4s`
        }
    }
}
</script>

<style>
.the-passage p {
  font-family: 'Smooch', cursive;
  font-size: 2.25rem;
}

.word {
    animation: appear;
    animation-duration: 2s;
    animation-fill-mode: initial;
}

@keyframes appear {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
</style>
