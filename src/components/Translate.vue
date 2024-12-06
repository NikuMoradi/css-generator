<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Translate" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="translate_x"
              label="Value X"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="translate_x_unitType"
              :options="translate_x_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="translate_y"
              label="Value Y"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="translate_y_unitType"
              :options="translate_y_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="translate-preview" :style="translatePreview">
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi cum
          voluptas autem officiis suscipit eius distinctio, porro quibusdam
          dolore quae saepe ipsum iste necessitatibus sunt quisquam rerum, unde
          vel eveniet impedit ratione soluta recusandae? Voluptas dolor ipsam
          aspernatur excepturi porro!
        </div>
      </div>
      <div class="code-box">{{ translateCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["translateEmit"],
  props: {
    translateProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const translate_x = ref("");
    const translate_y = ref("");
    const translate_x_unitType = ref("");
    const translate_x_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const translate_y_unitType = ref("");
    const translate_y_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const translatePreview = computed(() => {
      return {
        transform: `translate(${translate_x.value}${translate_x_unitType.value}, ${translate_y.value}${translate_y_unitType.value})`,
      };
    });
    const translateCode = computed(() => {
      if (
        translate_x.value !== "" &&
        translate_x_unitType.value !== "" &&
        translate_y.value !== "" &&
        translate_y_unitType.value !== ""
      ) {
        return `transform: translate(${translate_x.value}${translate_x_unitType.value}, ${translate_y.value}${translate_y_unitType.value});\n`;
      } else {
        return null;
      }
    });

    watch(translateCode, (newVal) => {
      ctx.emit("translateEmit", {
        type: "translate",
        code: newVal,
      });
    });

    const parseTranslateProp = () => {
      if (props.translateProp.transform) {
        const transform = props.translateProp.transform;
        const translateMatch = transform.match(
          /translate\((-?\d+)([a-z%]*),\s*(-?\d+)([a-z%]*)\)/
        );
        if (translateMatch) {
          translate_x.value = translateMatch[1] || "";
          translate_x_unitType.value = translateMatch[2] || "";
          translate_y.value = translateMatch[3] || "";
          translate_y_unitType.value = translateMatch[4] || "";
        }
      }
    };
    onMounted(() => {
      parseTranslateProp();
    });
    const clearObjItem = () => {
      translate_x.value = "";
      translate_y.value = "";
      translate_x_unitType.value = "";
      translate_y_unitType.value = "";
      translatePreview.value.transform = "";
    };

    return {
      translatePreview,
      translateCode,
      translate_x,
      translate_y,
      translate_x_unitType,
      translate_x_unitTypes,
      translate_y_unitType,
      translate_y_unitTypes,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped>
.translate-preview {
  width: 19rem;
  height: 16rem;
  padding: 1rem;
  background-color: #1976d239;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1rem;
}
</style>
