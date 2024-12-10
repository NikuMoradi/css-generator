<template>
  <SubHeader title="Image Shadow (Drop Shadow)" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-input label="Color" outlined v-model="filter_imageShadow_color" class="mb-10">
          <template v-slot:append>
            <div
              class="show-color"
              :style="{
                backgroundColor: filter_imageShadow_color,
              }"
            ></div>
            <q-popup-proxy cover transition-show="scale" transition-hide="scale">
              <q-color v-model="filter_imageShadow_color" no-header-tabs :palette="colorPalette" />
            </q-popup-proxy>
          </template>
        </q-input>

        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Horizonatal Offset</span
            ><span>{{ filter_imageShadow_horizonatal_offset }} px</span>
          </div>
          <q-slider
            v-model="filter_imageShadow_horizonatal_offset"
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
            <span>Vertical Offset</span><span>{{ filter_imageShadow_vertical_offset }} px </span>
          </div>
          <q-slider
            v-model="filter_imageShadow_vertical_offset"
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
            <span>Blur</span><span>{{ filter_imageShadow_blur }} px </span>
          </div>
          <q-slider
            v-model="filter_imageShadow_blur"
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
        <div class="drop-shadow-preview" :style="imageShadowPreview"></div>
      </div>

      <div class="code-box">{{ imageShadowCode }}</div>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['imageShadowEmit'],
  props: {
    imageShadowProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject('usedColors')
    const filter_imageShadow_color = ref('')
    const filter_imageShadow_horizonatal_offset = ref()
    const filter_imageShadow_vertical_offset = ref()
    const filter_imageShadow_blur = ref()

    const parseDropShadow = (filter) => {
      const regex = /drop-shadow\(\s*(-?\d+)px\s+(-?\d+)px\s+(\d+)px\s*(#[0-9a-fA-F]{6})?\s*\)/

      const matches = filter.match(regex)
      if (matches) {
        filter_imageShadow_horizonatal_offset.value = Number(matches[1])
        filter_imageShadow_vertical_offset.value = Number(matches[2])
        filter_imageShadow_blur.value = Number(matches[3])
        filter_imageShadow_color.value = matches[4] || ' '
      }
    }

    if (props.imageShadowProp.filter) {
      parseDropShadow(props.imageShadowProp.filter)
    }

    const imageShadowPreview = computed(() => {
      return {
        filter: `drop-shadow(${filter_imageShadow_horizonatal_offset.value}px ${filter_imageShadow_vertical_offset.value}px ${filter_imageShadow_blur.value}px ${filter_imageShadow_color.value})`,
      }
    })

    const imageShadowCode = computed(() => {
      if (
        filter_imageShadow_horizonatal_offset.value !== '' &&
        filter_imageShadow_vertical_offset.value !== '' &&
        filter_imageShadow_blur.value !== '' &&
        filter_imageShadow_horizonatal_offset.value !== undefined &&
        filter_imageShadow_vertical_offset.value !== undefined &&
        filter_imageShadow_blur.value !== undefined
      ) {
        return `filter: drop-shadow(${filter_imageShadow_horizonatal_offset.value}px ${filter_imageShadow_vertical_offset.value}px ${filter_imageShadow_blur.value}px ${filter_imageShadow_color.value});\n`
      } else return ''
    })

    watch(imageShadowCode, (newVal) => {
      ctx.emit('imageShadowEmit', {
        type: 'imageShadow',
        code: newVal,
      })
    })

    const clearObjItem = () => {
      filter_imageShadow_color.value = ''
      filter_imageShadow_horizonatal_offset.value = ''
      filter_imageShadow_vertical_offset.value = ''
      filter_imageShadow_blur.value = ''
      imageShadowPreview.value.filter = ''
    }
    // Watch filter_imageShadow_color to ensure it's always a valid hex color
    watch(filter_imageShadow_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        filter_imageShadow_color.value = '' // Reset to default color if invalid
      }
    })

    return {
      colorPalette,
      imageShadowPreview,
      imageShadowCode,
      filter_imageShadow_color,
      filter_imageShadow_horizonatal_offset,
      filter_imageShadow_vertical_offset,
      filter_imageShadow_blur,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.drop-shadow-preview {
  background: #ffff url('/assets/sample.jpg') center center/cover no-repeat scroll;
  width: 19rem;
  height: 16rem;
}
</style>
