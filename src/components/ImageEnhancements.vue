<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Image Enhancements" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Blur</span><span>{{ filter_blur }} px </span>
            </div>
            <q-slider
              v-model="filter_blur"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="100"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Brightness</span><span>{{ filter_brightness }} % </span>
            </div>
            <q-slider
              v-model="filter_brightness"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="300"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Contrast</span><span>{{ filter_contrast }} % </span>
            </div>
            <q-slider
              v-model="filter_contrast"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="100"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Grayscale</span><span>{{ filter_grayscale }} % </span>
            </div>
            <q-slider
              v-model="filter_grayscale"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="100"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Hue Rotate</span><span>{{ filter_hue_rotate }} deg </span>
            </div>
            <q-slider
              v-model="filter_hue_rotate"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="360"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Saturate</span><span>{{ filter_saturate }} % </span>
            </div>
            <q-slider
              v-model="filter_saturate"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="500"
              class="mb-10"
            ></q-slider>
          </div>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Sepia</span><span>{{ filter_sepia }} % </span>
            </div>
            <q-slider
              v-model="filter_sepia"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="100"
              class="mb-10"
            ></q-slider>
          </div>
        </div>
      </q-scroll-area>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="image-enhancements-Preview" :style="imageEnhancementsPreview"></div>
      </div>
      <div class="code-box">
        {{ imageEnhancementsCode }}
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['imageEnhancementsEmit'],
  props: {
    imageEnhancementsProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const filter_blur = ref()
    const filter_brightness = ref()
    const filter_contrast = ref()
    const filter_grayscale = ref()
    const filter_hue_rotate = ref()
    const filter_saturate = ref()
    const filter_sepia = ref()
    const imageEnhancementsPreview = computed(() => ({
      filter: `blur(${filter_blur.value}px) brightness(${filter_brightness.value}%) contrast(${filter_contrast.value}%) grayscale(${filter_grayscale.value}%) hue-rotate(${filter_hue_rotate.value}deg) saturate(${filter_saturate.value}%) sepia(${filter_sepia.value}%)\n`,
    }))
    const imageEnhancementsCode = computed(() => {
      if (
        filter_blur.value !== '' &&
        filter_brightness.value !== '' &&
        filter_contrast.value !== '' &&
        filter_grayscale.value !== '' &&
        filter_hue_rotate.value !== '' &&
        filter_saturate.value !== '' &&
        filter_sepia.value !== '' &&
        filter_blur.value !== undefined &&
        filter_brightness.value !== undefined &&
        filter_contrast.value !== undefined &&
        filter_grayscale.value !== undefined &&
        filter_hue_rotate.value !== undefined &&
        filter_saturate.value !== undefined &&
        filter_sepia.value !== undefined
      ) {
        return `filter: blur(${filter_blur.value}px) brightness(${filter_brightness.value}%) contrast(${filter_contrast.value}%) grayscale(${filter_grayscale.value}%) hue-rotate(${filter_hue_rotate.value}deg) saturate(${filter_saturate.value}%) sepia(${filter_sepia.value}%);\n`
      } else return ''
    })
    watch(imageEnhancementsCode, (newVal) => {
      ctx.emit('imageEnhancementsEmit', {
        type: 'imageEnhancements',
        code: newVal,
      })
    })
    const parseImageEnhancementsProp = () => {
      const filter = props.imageEnhancementsProp.filter || ''
      filter.split(' ').forEach((part) => {
        const value = Number(part.match(/\d+/))
        if (part.startsWith('blur')) filter_blur.value = value
        else if (part.startsWith('brightness')) filter_brightness.value = value
        else if (part.startsWith('contrast')) filter_contrast.value = value
        else if (part.startsWith('grayscale')) filter_grayscale.value = value
        else if (part.startsWith('hue-rotate')) filter_hue_rotate.value = value
        else if (part.startsWith('saturate')) filter_saturate.value = value
        else if (part.startsWith('sepia')) filter_sepia.value = value
      })
    }

    onMounted(() => {
      parseImageEnhancementsProp()
    })

    const clearObjItem = () => {
      filter_blur.value = ''
      filter_brightness.value = ''
      filter_contrast.value = ''
      filter_grayscale.value = ''
      filter_hue_rotate.value = ''
      filter_saturate.value = ''
      filter_sepia.value = ''
      imageEnhancementsPreview.value.filter = ''
    }

    return {
      imageEnhancementsPreview,
      imageEnhancementsCode,
      filter_blur,
      filter_brightness,
      filter_contrast,
      filter_grayscale,
      filter_hue_rotate,
      filter_saturate,
      filter_sepia,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.image-enhancements-Preview {
  background: #ffff url('/assets/sample.jpg') center center/cover no-repeat scroll;
  width: 19rem;
  height: 16rem;
}
</style>
