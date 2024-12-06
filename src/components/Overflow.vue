<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Overflow" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="overflow_x"
          :options="overflow_xs"
          label="Overflow_x"
          class="mb-10"
        />
        <q-select
          outlined
          v-model="overflow_y"
          :options="overflow_ys"
          label="Overflow_y"
          class="mb-10"
        />
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="overflow-preview" :style="overflowPreview">
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
          Lorem ipsum dolor sit amet adipisicing elit. Illum?<br />
        </div>
      </div>
      <div class="code-box">
        {{ overflowCode }}
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["overflowEmit"],
  props: {
    overflowProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const overflow_x = ref("");
    const overflow_xs = ["", "auto", "hidden", "scroll", "visible"];
    const overflow_y = ref("");
    const overflow_ys = ["", "auto", "hidden", "scroll", "visible"];
    const overflowPreview = computed(() => ({
      overflow: overflow_x.value,
      overflowY: overflow_y.value,
    }));
    const overflowCode = computed(() => {
      let code = "";
      if (overflow_x.value) {
        code += `overflow-x: ${overflow_x.value};\n`;
      }
      if (overflow_y.value) {
        code += `overflow-y: ${overflow_y.value};\n`;
      }

      return code;
    });

    watch(overflowCode, (newVal) => {
      ctx.emit("overflowEmit", { type: "overflow", code: newVal });
    });

    overflow_x.value = props.overflowProp["overflow-x"];
    overflow_y.value = props.overflowProp["overflow-y"];

    const clearObjItem = () => {
      overflow_x.value = "";
      overflow_y.value = "";
    };

    return {
      overflowPreview,
      overflowCode,
      overflow_x,
      overflow_xs,
      overflow_y,
      overflow_ys,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped>
.overflow-preview {
  background-color: #ffffff;
  width: 19rem;
  height: 16rem;
  border: 2px solid #1976d239;
  font-size: 1rem;
  line-height: 1.9;
  padding: 0.8rem;
  white-space: nowrap;
  overflow: hidden;
}
</style>
