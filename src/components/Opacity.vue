<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Opacity" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Value</span><span>{{ opacity_opacity }} </span>
          </div>
          <q-slider
            v-model="opacity_opacity"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :max="100"
            class="mb-10"
          ></q-slider>
        </div>
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="preview" :style="opacityPreview"></div>
      </div>
      <div class="code-box">{{ opacityCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from "vue";
import SubHeader from "./SubHeader.vue";
export default {
  emits: ["opacityEmit"],
  props: {
    opacityProp: {
      type: Object,
      required: false,
    },
  },

  setup(props, ctx) {
    const opacity_opacity = ref();
    const opacityPreview = computed(() => {
      return {
        opacity: `${opacity_opacity.value}%`,
      };
    });
    const opacityCode = computed(() => {
      if (opacity_opacity.value !== "" && opacity_opacity.value !== undefined) {
        return `opacity: ${opacity_opacity.value}%;\n`;
      } else {
        return "";
      }
    });
    watch(opacityCode, (newVal) => {
      ctx.emit("opacityEmit", { type: "opacity", code: newVal });
    });
    onMounted(() => {
      if (props.opacityProp.opacity) {
        opacity_opacity.value = Number(
          props.opacityProp.opacity.replace("%", "")
        );
      }
    });
    const clearObjItem = () => {
      opacity_opacity.value = "";
      opacityPreview.value.opacity = "";
    };

    return {
      opacityPreview,
      opacityCode,
      opacity_opacity,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped></style>
