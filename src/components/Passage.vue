<template>
    <div class="the-passage">
        <p>
            <span 
                v-for="word, index in passageInWords" 
                :key="genKey(word, index)" 
                class="word"
                :class="{ 'alt': flipCoin() }"
                :style="{ animationDelay: index + '500ms', fontSize: getRandomInt(2, 4) + 'rem' }"
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
        },
        genKey(word, index) {
            return `${word}-${index}`;
        },
        getRandomInt(min, max) {
            min = Math.ceil(min);
            max = Math.floor(max);
            return Math.floor(Math.random() * (max - min + 1)) + min;
        },
        flipCoin() {
            return Math.random() > 0.5 ? true : false;
        }
    }
}
</script>

<style>
.word {
    animation: appear;
    animation-duration: 2s;
    animation-fill-mode: forwards;
    opacity: 0;
    font-family: 'Comforter Brush', cursive;
    font-size: 2.25rem;
}

.word.alt {
    font-family: 'Permanent Marker', cursive;
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
