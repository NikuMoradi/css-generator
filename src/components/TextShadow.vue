<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Text Shadow" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-input
          label="Color"
          outlined
          v-model="textShadow_color"
          class="mb-10"
        >
          <template v-slot:append>
            <div
              class="show-color"
              :style="{ backgroundColor: textShadow_color }"
            ></div>
            <q-popup-proxy
              cover
              transition-show="scale"
              transition-hide="scale"
            >
              <q-color
                v-model="textShadow_color"
                no-header-tabs
                :palette="colorPalette"
              />
            </q-popup-proxy>
          </template>
        </q-input>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Horizontal Offset</span
            ><span>{{ textShadow_horizontal_offset }} px </span>
          </div>
          <q-slider
            v-model="textShadow_horizontal_offset"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="-100"
            :max="100"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Vertical Offset</span
            ><span>{{ textShadow_vertical_offset }} px </span>
          </div>
          <q-slider
            v-model="textShadow_vertical_offset"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="-100"
            :max="100"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Blur</span><span>{{ textShadow_blur }} px </span>
          </div>
          <q-slider
            v-model="textShadow_blur"
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
        <div class="text-shadow-preview" :style="textShadowPreview">
          Text Shadow
        </div>
      </div>
      <div class="code-box">
        {{ textShadowCode }}
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted, inject } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["textShadowEmit"],
  props: {
    textShadowProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject("usedColors");

    const textShadow_color = ref("");
    const textShadow_horizontal_offset = ref();
    const textShadow_vertical_offset = ref();
    const textShadow_blur = ref();
    watch(textShadow_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        textShadow_color.value = "";
      }
    });
    const textShadowPreview = computed(() => {
      return {
        textShadow: `${textShadow_horizontal_offset.value}px ${textShadow_vertical_offset.value}px  ${textShadow_blur.value}px ${textShadow_color.value}`,
      };
    });
    const textShadowCode = computed(() => {
      if (
        textShadow_horizontal_offset.value !== "" &&
        textShadow_vertical_offset.value !== "" &&
        textShadow_blur.value !== "" &&
        textShadow_horizontal_offset.value !== undefined &&
        textShadow_vertical_offset.value !== undefined &&
        textShadow_blur.value !== undefined
      ) {
        return `text-shadow: ${textShadow_horizontal_offset.value}px ${textShadow_vertical_offset.value}px ${textShadow_blur.value}px ${textShadow_color.value};\n`;
      } else return "";
    });

    watch(textShadowCode, (newVal) => {
      ctx.emit("textShadowEmit", { type: "textShadow", code: newVal });
    });
    const parseTextShadow = (style) => {
      const regex = /(\d+)px\s(\d+)px\s(\d+)px\s?(#\w+)?/;

      const matches = style.match(regex);

      if (matches) {
        textShadow_horizontal_offset.value = Number(matches[1]);
        textShadow_vertical_offset.value = Number(matches[2]);
        textShadow_blur.value = Number(matches[3]);
        textShadow_color.value = matches[4] || "";
      }
    };
    onMounted(() => {
      if (props.textShadowProp["text-shadow"]) {
        parseTextShadow(props.textShadowProp["text-shadow"]);
      }
    });

    const clearObjItem = () => {
      textShadow_color.value = "";
      textShadow_horizontal_offset.value = "";
      textShadow_vertical_offset.value = "";
      textShadow_blur.value = "";
      textShadowPreview.value.textShadow = "";
    };
    return {
      colorPalette,
      textShadowPreview,
      textShadowCode,
      textShadow_color,
      textShadow_horizontal_offset,
      textShadow_vertical_offset,
      textShadow_blur,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped>
.text-shadow-preview {
  font-size: 1.9rem;
}
</style>
