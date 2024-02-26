<template>
  <div class="weddings-list">
    <h2>Брачные союзы</h2>
      <span v-for="(wedding, index) in weddings" :key="index">
        <div class="wedding-item">
          <strong>{{ wedding.person.name }}</strong>
          <span v-if="wedding.date_end">
            ({{ wedding.date_start }}-{{ wedding.date_end }})
          </span>
          <span v-else>
            ({{ wedding.date_start }})
        </span>
        </div>
      </span>
  </div>
</template>

<script>
export default {
  name: 'WeddingsList',
  props: {
    weddings: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped lang="less">
.wedding-item {
  background-color: #f2f2f2;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
  text-align: center;
  max-width: 400px;
  font-family: Arial;
  font-weight: 600;
}
</style>