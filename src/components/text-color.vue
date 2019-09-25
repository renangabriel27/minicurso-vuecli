<template>
  <div class="form-group">
    <label>TEXT COLOR</label>
    <span
      v-for="(color, index) in colors"
      :key="index"
    >
      <span
        id="span-color"
        :style="{ background: color }"
        @click="emitUpdateTextColor(color)"
      >
      </span>
    </span>
  </div>
</template>

<script>
export default {
  name: 'TextColor',

  props: {
    colors: {
      type: Array,
      required: true
    },
  },

  methods: {
    emitUpdateTextColor(color) {
      this.$root.$emit('update-text-color', color);
    },
  },
};
</script>

<style scoped>

#span-color {
  border: 1px solid #000;
  border-radius: 50%;
  cursor: pointer;
  display: inline-block;
  width: 16px;
  height: 16px;
  margin-left: 3px;
}

</style>
