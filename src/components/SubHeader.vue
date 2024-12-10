<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="row wrapper">
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
  gap: 0.7rem;
}
.title {
  font-size: 1.5rem;
  font-weight: 500;
}
.clear-btn {
  padding: 0.5;
  font-size: 0.7rem;
  background-color: #f8e6e57a;
}
@media (max-width: 1024px) {
  .wrapper {
    justify-content: space-between;
  }
}
</style>
