<template>
  <div class="input-helper">
    <div v-for="option in options" :key="option" class="input-helper__item" @click="() => selectOption(option)">
      {{ option }}
    </div>
  </div>
</template>
    
<script>
export default {
  props: {
    options: {
      type: Array,
      required: true
    }
  },
  methods: {
    selectOption(value) {
      this.$emit('select', value);
    }
  }
}
</script>
    
<style scoped lang = "less">
.input-helper {
  background-color: #f5f5f5;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 10px;

  &__item {
    cursor: pointer;
    padding: 5px;  

    &:hover {
      background-color: #e0e0e0; 
    }
  }
}
</style>
  