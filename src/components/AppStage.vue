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
          <span v-for="option in types" :key="option.name" class="type-select">
            {{ option.name }}
          </span>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'AppStage',
  props: {
    msg: String
  },
  data() {
    return {
      app: 'Annihilipsum Generator',
      passage: 'Where lies the strangling fruit that came from the hand of the sinner I shall bring forth the seeds of the dead to share with the worms that gather in the darkness and surround the world with the power of their lives while from the dim-lit halls of other places forms that never could be writhe for the impatience of the few who have never seen or been seen. In the black water with the sun shining at midnight, those fruit shall come ripe and in the darkness of that which is golden shall split open to reveal the revelation of the fatal softness in the earth. The shadows of the abyss are like the petals of a monstrous flower that shall blossom within the skull and expand the mind beyond what any man can bear...',
      type: {
        word: false,
        sentence: false,
        paragraph: true,
      },
      types: [
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
    this.focusInput()
  },
  methods: {
    focusInput() {
      this.$refs.count.focus()
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.selections {
  display: flex;
  justify-content: space-between;
}

label {
  display: block;
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
