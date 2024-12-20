<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="wrapper">
    <p class="title">{{ title }}</p>
    <q-btn color="red-11" icon="fas fa-trash" flat dense class="clear-btn" @click="onClear" />
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    onClear: {
      type: Function,
      required: true,
    },
  },
}
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: baseline;
  gap: 0.75rem;
}
.title {
  font-size: 1.5rem;
  font-weight: 500;
}
.clear-btn {
  font-size: 0.7rem;
  background-color: #f8e6e57a;
  padding: 0.5rem;

  border-radius: 10px;
}
@media (max-width: 1024px) {
  .wrapper {
    justify-content: space-between;
    align-items: stretch;
    padding: 0.5rem;
  }
  .clear-btn {
    font-size: 0.7rem;
    background-color: #f8e6e57a;
    padding: 1rem;
    border-radius: 10px;
  }
}
</style>
