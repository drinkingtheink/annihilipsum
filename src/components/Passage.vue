<template>
    <div class="the-passage">
        <p 
            v-if="preppedPassage"
            @click="goToInfoLink()"
        >
            <transition-group name="words" tag="span">
                <span 
                    v-for="word, index in preppedPassage" 
                    :key="genKey(word, index)"
                    class="word"
                    :class="{ 'alt': flipCoin(), 'alt2': flipCoin(), 'rotate': flipCoin(), 'blurred': flipCoin(), 'blue-green': flipCoin(), 'need-help': flipCoin(), 'need-drop': flipCoin() }"
                    :style="{ animationDelay: index + '50ms', fontSize: getRandomInt(2, 4) + 'rem' }"
                >
                    {{ word }}
                </span>
            </transition-group>
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
    data() {
        return {
            preppedPassage: null,
            aboutIncantationLink: 'https://southernreach.fandom.com/wiki/Tower_incantation',
        }
    },
    mounted() {
        if (this.passageInWords) {
            this.preppedPassage = this.passageInWords;
        }

        setInterval(() => {
            console.log(`CLEARING PREPPED PASSAGE >>>>>>>>>>>>>>>>`);
            this.clearWords();
        }, 20000);
    },
    methods: {
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
        },
        goToInfoLink() {
            window.open(this.aboutIncantationLink);
        },
        clearWords() {
            this.preppedPassage = null;

            setTimeout(() => {
                this.preppedPassage = this.passageInWords;
            }, 40000);
        }
    }
}
</script>

<style>
.word {
    animation: appear;
    animation-duration: 2s;
    animation-fill-mode: both;
    animation-direction: alternate;
    opacity: 0;
    font-family: 'Comforter Brush', cursive;
    font-size: 2.25rem;
    color: #EE9B00;
    transition: all .2s;
    display: inline-block;
    margin-right: 8px;
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

.word.blue-green {
    color: #0A9396;
}

.word.need-help {
    cursor: help;
}

.word.need-wait {
    cursor: wait;
}

.word.need-drop {
    cursor: no-drop;
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
        transform: translateY(-20px);
    }
    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

.words-leave-active {
  transition: all 1s;
}
.words-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
