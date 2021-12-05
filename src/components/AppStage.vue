<template>
  <main>
    <h1>{{ app }}</h1>

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
    </section>

    <section class="generated">

    </section>

    <section class="the-passage">
      <p>{{ passage }}</p>
    </section>
  </main>
</template>

<script>
const defaultType = 'paragraphs';
const defaultCount = 1;

export default {
  name: 'AppStage',
  props: {
    msg: String
  },
  data() {
    return {
      app: 'Annihilipsum Generator',
      passage: 'Where lies the strangling fruit that came from the hand of the sinner I shall bring forth the seeds of the dead to share with the worms that gather in the darkness and surround the world with the power of their lives while from the dim-lit halls of other places forms that never could be writhe for the impatience of the few who have never seen or been seen. In the black water with the sun shining at midnight, those fruit shall come ripe and in the darkness of that which is golden shall split open to reveal the revelation of the fatal softness in the earth. The shadows of the abyss are like the petals of a monstrous flower that shall blossom within the skull and expand the mind beyond what any man can bear...',
      type: null,
      typeOptions: [
        {
          name: 'words'
        },
        {
          name: 'sentences'
        },
        {
          name: 'paragraphs'
        }
      ],
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
