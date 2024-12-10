<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Visibility" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="visibility_visibility"
          :options="visibility_visibilitys"
          label="Value"
          class="mb-10"
        />
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="preview" :style="visibilityPreview">
          This box is visible!
        </div>
      </div>
      <div class="code-box">{{ visibilityCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["visibilityEmit"],
  props: {
    visibilityProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const visibility_visibility = ref("");
    const visibility_visibilitys = ["", "visible", "hidden"];
    const visibilityPreview = computed(() => {
      return {
        visibility: `${visibility_visibility.value}`,
      };
    });
    const visibilityCode = computed(() => {
      if (visibility_visibility.value) {
        return `visibility:  ${visibility_visibility.value};\n`;
      } else return "";
    });

    watch(visibilityCode, (newVal) => {
      ctx.emit("visibilityEmit", { type: "visibility", code: newVal });
    });
    visibility_visibility.value = props.visibilityProp.visibility;

    const clearObjItem = () => {
      visibility_visibility.value = "";
    };
    return {
      visibilityPreview,
      visibilityCode,
      visibility_visibility,
      visibility_visibilitys,
      clearObjItem,
    };
  },

  components: {
    SubHeader,
  },
};
</script>

<style scoped></style>
