<template>
  <main>
    <h1>{{ app }}</h1>

    <section class="description-stage">
      <SRLogo  class="sr-logo" />
      <p class="description">Provide lifelike text for your prototyping projects while simultaneously <em>conditioning your end users for the physically and psychologically exhaustive process of crossing into Area X</em>. - <a href="https://southernreach.fandom.com/wiki/Southern_Reach" target="_blank">The Southern Reach</a></p>
    </section>

    <section class="generated-stage">
      <div class="toolbox">
        <section class="selections">
          <div>
            <label for="count">How Many?</label>
            <input type="number" id="count" ref="count" @change="genText()" />
          </div>

          <div>
            <label for="count">Of What?</label>
          
            <div class="type-selection">
              <button 
                v-for="option in typeOptions" 
                :key="option.name" 
                class="type-select"
                :class="{ 'active': option.name === type }"
                @click="setType(option.name)"
              >
                {{ option.name }}
              </button>
            </div>
          </div>
        </section>

        <section class="generated">
            <div v-if="!formattedFinalText" class="toolbox-sr-logo">
              <SRLogo class="toolbox-sr" />
              <p>Something went wrong, try a different request.<br/> - The Southern Reach</p>
            </div>
            
            <p 
              v-if="formattedFinalText"
              ref="generator"
              class="final-text"
              id="final-text"
              v-html="formattedFinalText"
              tabindex="0"
            ></p><span class="blinking-cursor">|</span>
        </section>

        <div class="text-actions">
            <button 
              class="copy-text"
              :class="{ 'confirm-copy': confirmCopy }"
              v-clipboard:copy="textForCopying"
              v-clipboard:success="onCopy"
              v-clipboard:error="onError"
            >{{ confirmCopy ? 'Text Copied!' : 'Copy Text' }}</button>

            <a 
              href="https://www.jeffvandermeer.com/book/area-x/"
              target="_blank"
            >WTF?</a>

            <a 
              href="https://github.com/drinkingtheink/annihilipsum"
              target="_blank"
            >About this Project</a>

            <a 
              href="https://drinkingtheink.github.io/"
              target="_blank"
            >About the Author</a>
        </div>
      </div>
    </section>

    <Passage 
      :passage="passage"
      :passageInWords="passageForCrawler"
     />
  </main>
</template>

<script>
import Passage from './Passage.vue';
import SRLogo from './SRLogo.vue';

const defaultType = 'sentences';
const defaultCount = 6;

export default {
  name: 'AppStage',
  components: {
    Passage,
    SRLogo
  },
  data() {
    return {
      app: 'Annihil·ipsum Generator',
      passage: 'Where lies the strangling fruit that came from the hand of the sinner I shall bring forth the seeds of the dead to share with the worms that gather in the darkness and surround the world with the power of their lives while from the dimlit halls of other places forms that never were and never could be writhe for the impatience of the few who never saw what could have been. In the black water with the sun shining at midnight, those fruit shall come ripe and in the darkness of that which is golden shall split open to reveal the revelation of the fatal softness in the earth. The shadows of the abyss are like the petals of a monstrous flower that shall blossom within the skull and expand the mind beyond what any man can bear, but whether it decays under the earth or above on green fields, or out to sea or in the very air, all shall come to revelation, and to revel, in the knowledge of the strangling fruit—and the hand of the sinner shall rejoice, for there is no sin in shadow or in light that the seeds of the dead cannot forgive. And there shall be in the planting in the shadows a grace and a mercy from which shall blossom dark flowers, and their teeth shall devour and sustain and herald the passing of an age. That which dies shall still know life in death for all that decays is not forgotten and reanimated it shall walk the world in the bliss of not-knowing. And then there shall be a fire that knows the naming of you, and in the presence of the strangling fruit, its dark flame shall acquire every part of you that remains.',
      type: null,
      typeOptions: [
        {
          name: 'paragraphs'
        },
        {
          name: 'sentences'
        },
        {
          name: 'words'
        }
      ],
      finalText: null,
      confirmCopy: false,
      error: false,
    }
  },
  computed: {
    passageForCrawler() {
      return this.passage.split(' ');
    },
    passageInSentences() {
      return this.passage.replace(/([.?!])\s*(?=[A-Z])/g, "$1|").split("|");
    },
    passageInWords() {
      return this.passage.split(' ');
    },
    formattedFinalText() {
      let newFinalText;

      newFinalText = this.finalText;
      
      return newFinalText ? newFinalText : null;
    },
    textForCopying() {
      let origString = `${this.formattedFinalText}`;
      let formattedString = origString.replace(/(<([^>]+)>)/gi, "\n");

      return formattedString;
    }
  },
  watch: {
    confirmCopy: function() {
      if (this.confirmCopy) {
        setTimeout(() => this.confirmCopy = false, 1000);
      }
    },
    type: function() {
      this.genText();
    },
    formattedFinalText: function() {
      let generatorEl = document.querySelector('.generated');
      if (generatorEl) {
        let scrollHeight = generatorEl.scrollHeight * 2;
        generatorEl.scrollTop = scrollHeight;
      } 
    }
  },
  mounted() {
    this.setType(defaultType);
    this.$refs.count.value = defaultCount;
    this.genText();
    this.focusInput();
  },
  methods: {
    focusInput() {
      this.$refs.count.focus();
    },
    setType(type) {
      this.type = type;
    },
    genText() {
      this.error = false;
      let textTypeCount = this.$refs.count.value;

      if (this.type === 'paragraphs' && textTypeCount == 1) {
        this.finalText = this.passage.toString();

      } else if (this.type === 'paragraphs' && textTypeCount > 1) {
        let currentParagraphs = `${this.passage}`;
        
        for (let step = 0; step < textTypeCount; step++) {
          currentParagraphs = currentParagraphs + '</p><p>' + this.passage;
        }

        this.finalText = currentParagraphs;
        
      } else if (this.type === 'sentences' && (textTypeCount <= this.passageInSentences.length)) {
        this.finalText = this.passageInSentences.slice(0, textTypeCount).join('</p><p>').toString();

      } else if (this.type === 'sentences' && (textTypeCount > this.passageInSentences.length)) {
        let currentSentences = [...this.passageInSentences];
        let howManyTimes = textTypeCount - this.passageInSentences.length;

        for (let step = 0; step < howManyTimes; step++) {
          this.passageInSentences.forEach((passage) => {
            currentSentences.push(passage);
          })
        }

        this.finalText = currentSentences.slice(0, textTypeCount).join('</p><p>').toString();

      } else if (this.type === 'words' && (textTypeCount < this.passageInWords.length)) {
        // using words so get words
        this.finalText = this.passageInWords.slice(0, textTypeCount).join(' ');

      }
    },
    onCopy() {
      this.confirmCopy = true;
    },
    onError() {
      this.error = true;
      console.log(` An error occured trying to copy the text. Please try again. - The Southern Reach `);
    },
  },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@500&display=swap');

main {
  position: relative;
}

h1 {
  text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.3);
}

.description-stage {
  display: flex;
  justify-content: center;
  margin: 0 auto;
  max-width: 700px;
}

.description-stage .sr-logo {
  width: 10rem;
  margin-right: 1rem;
}

.description {
  color: #001219;
  font-weight: bold;
  font-size: 1.1rem;
  text-align: left;
  border-left: 1px solid rgba(0,0,0,0.5);
  padding-left: 1rem;
}

.selections {
  display: flex;
  justify-content: space-around;
}

.selections div {
  text-align: left;
}

label {
  display: block;
  text-align: left;
  text-transform: uppercase;
  font-weight: bold;
  color: #EE9B00;
}

.type-select {
  margin-right: 0.5rem;
}

.type-select.active {
  background-color: red;
}

.generated-stage {
  display: flex;
  justify-content: center;
  position: relative;
}

.toolbox {
  width: 700px;
  border: 5px solid rgba(0,0,0,0.2);
  border-radius: 10px;
  padding: 0.5rem 1rem;
  background-color: #005F73;
  z-index: 10;
  position: relative;
  box-shadow: 1px 8px 15px 5px rgba(0,0,0,0.6);
  transition: all .2s;
}

.generated {
  background-color: #e0e0e0;
  margin: 1rem 0 0.5rem 0;
  padding: 0.5rem 1.5rem;
  border-radius: 10px;
  position: relative;
  text-align: left;
  border: 5px solid rgba(0,0,0,0.2);
  min-height: 10rem;
  max-height: 450px;
  overflow: auto;
  scroll-behavior: smooth;
}

.generated .final-text {
  margin: 0;
  padding: 0;
  font-family: 'Roboto Mono', monospace;
}

.generated .text-actions {
  border-top: 1px solid rgba(0,0,0,0.2);
  padding: 0.5rem 0;
}

@keyframes screenFlicker {
  0%   { 
    filter: blur(2px);
  }
  20%  { 
    filter: blur(0);
  }
  25%  { 
    filter: blur(1px);
  }
  80% { 
    filter: blur(0); 
  }
}

.generated .toolbox-sr-logo {
  text-align: center;
  width: 100%;
  animation: screenFlicker 2s 2s infinite;
}

.toolbox-sr-logo p {
  font-family: 'Roboto Mono', monospace;
}

.toolbox-sr {
  width: 12rem;
  opacity: 0.1;
}

.text-actions a {
  margin: 0 1rem;
  color: white;
  text-decoration: none;
}

.text-actions a:hover {
  color: red;
}

button.copy-text {
  margin-right: 2rem;
  width: 13rem;
}

button.copy-text.confirm-copy {
  padding-left: 3rem;
  padding-right: 3rem;
  background-color: #94D2BD;
  color: red;
}

.the-passage {
  position: absolute;
  top: 25rem;
  left: 0;
  right: 0;
  margin: auto;
  z-index: 1;
  max-width: 1300px;
}

input {
  font-size: 2rem;
}

input[type="number"] {
  width: 5rem;
  text-align: center;
  border-radius: 10px;
  border: 3px solid rgba(0,0,0,0.4);
  color: red;
  font-family: 'Permanent Marker', cursive;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: white;
}

@keyframes blink {
  from, to {
    color: transparent;
  }
  50% {
    color: black;
  }
}

.blinking-cursor {
  font-weight: 800;
  color: #2E3D48;
  animation: 1s blink step-end infinite;
}
</style>
