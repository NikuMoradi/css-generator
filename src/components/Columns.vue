<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Columns" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Number of Columns</span><span>{{ column_count }}</span>
          </div>
          <q-slider
            v-model="column_count"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="1"
            :max="50"
            class="mb-10"
          ></q-slider>
        </div>
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="column-preview" :style="columnPreview">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. In earum
          itaque eos, ullam quod maiores nulla dignissimos temporibus repellat
          atque, tenetur voluptate nesciunt! Quasi quae suscipit, odio
          aspernatur hic commodi, ab voluptatum laborum ducimus sapiente saepe.
          Nam delectus neque facere ab illo! Quae, saepe molestiae sapiente
          magni eligendi id itaque perferendis iure velit, veniam voluptate
          harum consectetur reiciendis libero laboriosam eaque magnam est
          repudiandae. Cupiditate at laborum error, odio laudantium recusandae
          minima adipisci alias mollitia commodi non velit quis ducimus est
          dignissimos voluptatibus. Quaerat, aliquam ipsam, incidunt fuga
          consequatur distinctio odit voluptatem voluptates rem at nobis atque
          qui autem dolore.
        </div>
      </div>

      <div class="code-box">{{ columnCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["columnsEmit"],
  props: {
    columnsProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const column_count = ref();
    const columnPreview = computed(() => {
      return {
        columnCount: `${column_count.value}`,
      };
    });
    const columnCode = computed(() => {
      if (column_count.value !== undefined && column_count.value !== "") {
        return `column-count: ${column_count.value};\n`;
      } else return "";
    });

    watch(columnCode, (newVal) => {
      ctx.emit("columnsEmit", { type: "columns", code: newVal });
    });
    onMounted(() => {
      if (props.columnsProp["column-count"]) {
        column_count.value = Number(props.columnsProp["column-count"]);
      }
    });

    const clearObjItem = () => {
      column_count.value = "";
    };
    return {
      columnPreview,
      columnCode,
      column_count,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped>
.column-preview {
  width: 90%;
  height: 90%;
  line-height: 1.9;
  overflow: hidden;
}
</style>
