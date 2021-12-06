<template>
  <main>
    <h1>{{ app }}</h1>

    <p>Provide "lifelike" text for your prototyping projects while simultaneously preparing your end users for the physically and psychologically exhaustive process of crossing into Area X. Win-win!</p>

    <section class="selections">
      <div>
        <label for="count">How Many?</label>
        <input type="number" id="count" ref="count" />
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

      <div>
          <button 
            id="get-text"
            @click="getText()"
          >Get Text</button>
      </div>
    </section>

    <section class="generated">

    </section>

    <Passage 
      :passage="passage"
      :passageInWords="passageForCrawler"
     />
  </main>
</template>

<script>
import Passage from './Passage.vue';

const defaultType = 'sentences';
const defaultCount = 6;

export default {
  name: 'AppStage',
  components: {
    Passage
  },
  props: {
    msg: String
  },
  data() {
    return {
      app: 'Annihilipsum Generator',
      passage: 'Where lies the strangling fruit that came from the hand of the sinner I shall bring forth the seeds of the dead to share with the worms that gather in the darkness and surround the world with the power of their lives while from the dimlit halls of other places forms that never were and never could be writhe for the impatience of the few who never saw what could have been. In the black water with the sun shining at midnight, those fruit shall come ripe and in the darkness of that which is golden shall split open to reveal the revelation of the fatal softness in the earth. The shadows of the abyss are like the petals of a monstrous flower that shall blossom within the skull and expand the mind beyond what any man can bear, but whether it decays under the earth or above on green fields, or out to sea or in the very air, all shall come to revelation, and to revel, in the knowledge of the strangling fruit—and the hand of the sinner shall rejoice, for there is no sin in shadow or in light that the seeds of the dead cannot forgive. And there shall be in the planting in the shadows a grace and a mercy from which shall blossom dark flowers, and their teeth shall devour and sustain and herald the passing of an age. That which dies shall still know life in death for all that decays is not forgotten and reanimated it shall walk the world in the bliss of not-knowing. And then there shall be a fire that knows the naming of you, and in the presence of the strangling fruit, its dark flame shall acquire every part of you that remains.',
      type: null,
      typeOptions: [
        {
          name: 'words'
        },
        {
          name: 'sentences'
        }
      ],
      finalText: null,
    }
  },
  computed: {
    passageForCrawler() {
      return this.passage.split(' ');
    },
    passageInWords() {
      return this.masterPassageInWords.split('. ').filter(function(n){return n; });
    },
    passageInSentences() {
      return this.masterPassageInSentences.split('. ').filter(function(n){return n; });
    },
    masterPassageInSentences() {
      return [...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences, ...this.passageInSentences];
    },
    masterPassageInWords() {
      return [...this.passageInWords, ...this.passageInWords, ...this.passageInWords, ...this.passageInWords, ...this.passageInWords, ...this.passageInWords, ...this.passageInWords, ...this.passageInWords];
    }
  },
  mounted() {
    this.setType(defaultType);
    this.$refs.count.value = defaultCount;
    this.focusInput();
  },
  methods: {
    focusInput() {
      this.$refs.count.focus();
    },
    setType(type) {
      this.type = type;
    },
    getText() {
      console.log(`GENNING TEXT >>>>>>>>>>>>>>>>>`);
      let text;
      let textTypeCount = this.$refs.count.value;

      if (this.type === 'sentences') {
        text = this.passageInSentences.slice(textTypeCount);
      } else {
        text = this.passageInWords.slice(textTypeCount);
      }

      return text;
    }
  },
}
</script>

<style scoped>
.selections {
  display: flex;
  justify-content: space-around;
}

label {
  display: block;
  text-align: left;
}

.type-select {
  text-transform: uppercase;
  border: 1px solid grey;
  border-radius: 10px;
  padding: 0.5rem 1rem;
  transform: all .2s;
  margin-right: 0.5rem;
}

.type-select:hover {
  background-color: black;
  color: white;
  cursor: pointer;
}

.type-select.active {
  background-color: red;
}

.generated {
  min-height: 15rem;
  background-color: #ccc;
  margin: 2rem 0;
}

input {
  font-size: 2rem;
}

input[type="number"] {
  width: 3rem;
  text-align: center;
  border-radius: 10px;
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
  color: #42b983;
}
</style>
