<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Skew" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Value X</span><span>{{ skew_x }} deg </span>
          </div>
          <q-slider
            v-model="skew_x"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="-90"
            :max="90"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Value Y</span><span>{{ skew_y }} deg</span>
          </div>
          <q-slider
            v-model="skew_y"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="-90"
            :max="90"
            class="mb-10"
          ></q-slider>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="skew-preview" :style="skewPreview">
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi cum voluptas autem officiis
          suscipit eius distinctio, porro quibusdam dolore quae saepe ipsum iste necessitatibus sunt
          quisquam rerum, unde vel eveniet impedit ratione soluta recusandae? Voluptas dolor ipsam
          aspernatur excepturi porro!
        </div>
      </div>
      <div class="code-box">{{ skewCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['skewEmit'],
  props: {
    skewProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const skew_x = ref()
    const skew_y = ref()
    const skewPreview = computed(() => {
      return {
        transform: `skew(${skew_x.value}deg, ${skew_y.value}deg)`,
      }
    })
    const skewCode = computed(() => {
      if (
        skew_x.value !== '' &&
        skew_y.value !== '' &&
        skew_x.value !== undefined &&
        skew_y.value !== undefined
      ) {
        return `transform: skew(${skew_x.value}deg, ${skew_y.value}deg);\n`
      } else return ''
    })

    watch(skewCode, (newVal) => {
      ctx.emit('skewEmit', {
        type: 'skew',
        code: newVal,
      })
    })

    const parseSkewProp = () => {
      if (props.skewProp.transform) {
        const transform = props.skewProp.transform
        const skewMatch = transform.match(/skew\((-?\d+)deg,\s*(-?\d+)deg\)/)
        if (skewMatch) {
          skew_x.value = Number(skewMatch[1])
          skew_y.value = Number(skewMatch[2])
        }
      }
    }

    onMounted(() => {
      parseSkewProp()
    })
    const clearObjItem = () => {
      skew_x.value = ''
      skew_y.value = ''
      skewPreview.value.transform = ''
    }

    return {
      skewPreview,
      skewCode,
      skew_x,
      skew_y,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.skew-preview {
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
