<template>
    <div class="the-passage">
        <p>
            <span 
                v-for="word, index in passageInWords" 
                :key="genKey(word, index)" 
                class="word"
                :class="{ 'alt': flipCoin(), 'alt2': flipCoin(), 'rotate': flipCoin(), 'blurred': flipCoin() }"
                :style="{ animationDelay: index + '50ms', fontSize: getRandomInt(2, 4) + 'rem' }"
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
            return Math.random() > 0.8 ? true : false;
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
    color: #EE9B00;
    transition: all .2s;
}

.word:hover {
    color: red;
    filter: blur(0);
}

.word.alt {
    font-family: 'Permanent Marker', cursive;
}

.word.alt2 {
    font-family: 'Smooch', cursive;
    display: inline-block;
    transform: rotate(5deg);
}

.rotate {
    transform: rotate(5deg);
}

.blurred {
    filter: blur(4px);
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
