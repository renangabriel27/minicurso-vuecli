<template>
  <div class="row m-0 py-2 text-center">
    <div id="main-content" class="col-md-6 d-block mx-auto position relative">
      <p class="fixed-top text" :style="textColor">
        {{ text.top }}
      </p>

      <img id="main-image" :src="image.path" :title="image.title">

      <p class="fixed-bottom text" :style="textColor">
        {{ text.bottom }}
      </p>
    </div>

    <div class="col-md-6">
      <h1 v-if="showTitle" class="mt-2">
        {{ titleFormatted }}
      </h1>

      <div class="form-group">
        <input
          type="text"
          placeholder="Top text"
          class="form-control"
          v-model="text.top"
          >
      </div>

      <div class="form-group">
        <input
          type="text"
          placeholder="Bottom text"
          class="form-control"
          v-model="text.bottom"
        >
      </div>

      <text-color :colors="colors" />

      <button
        class="btn btn-outline-primary"
        @click="resetInputs()"
      >
        Reset
      </button>
    </div>
  </div>
</template>

<script>

import TextColor from './text-color.vue';

export default {
  name: 'MemeGenerator',

  components: {
    TextColor
  },

  data() {
    return {
      title: '',
      showTitle: true,
      image: {
        path: 'https://imgflip.com/s/meme/I-Have-No-Idea-What-I-Am-Doing-Dog.jpg',
        title: 'I have no idea what I am doing'
      },
      text: {
        top: '',
        bottom: '',
        color: 'white'
      },
      colors: ['black', 'red', 'white'],
    };
  },

  computed: {
    titleFormatted() {
      return this.title.toUpperCase();
    },

    textColor() {
      return { color: this.text.color };
    },
  },

  created() {
    this.setTitle();
    this.onUpdateTextColor();
  },

  methods: {
    setTitle() {
      this.title = 'Meme Generator';
    },

    resetInputs() {
      this.text.top = '';
      this.text.bottom = '';
      this.text.color = 'white';
    },

    onUpdateTextColor() {
      this.$root.$on('update-text-color', (color) => {
        this.updateTextColor(color);
      })
    },

    updateTextColor(color) {
      this.text.color = color;
    },
  },
};

</script>

<style scoped>

#main-content {
  word-wrap: break-word;
}

#main-image {
  width: 100%;
  height: auto;
  max-height: 800px;
}

.text {
  color: #fff;
  font-family: 'Passion One';
  font-size: 4.5vw;
  line-height: 3.8vw;
  padding: 15px;
  position: absolute;
  text-transform: uppercase;
  text-shadow: 3px 3px 3px #000;
}

</style>
