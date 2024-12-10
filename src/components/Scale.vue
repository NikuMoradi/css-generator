<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Scale" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Value X</span><span>{{ scale_x }} </span>
          </div>
          <q-slider
            v-model="scale_x"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :step="0.1"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Value Y</span><span>{{ scale_y }} </span>
          </div>
          <q-slider
            v-model="scale_y"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :step="0.1"
            class="mb-10"
          ></q-slider>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="scale-preview" :style="scalePreview">
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi cum voluptas autem officiis
          suscipit eius distinctio, porro quibusdam dolore quae saepe ipsum iste necessitatibus sunt
          quisquam rerum, unde vel eveniet impedit ratione soluta recusandae? Voluptas dolor ipsam
          aspernatur excepturi porro!
        </div>
      </div>
      <div class="code-box">{{ scaleCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['scaleEmit'],
  props: {
    scaleProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const scale_x = ref()
    const scale_y = ref()
    const scalePreview = computed(() => {
      return {
        transform: `scale(${scale_x.value}, ${scale_y.value})`,
      }
    })
    const scaleCode = computed(() => {
      if (
        scale_x.value !== '' &&
        scale_x.value !== undefined &&
        scale_y.value !== '' &&
        scale_y.value !== undefined
      ) {
        return `transform: scale(${scale_x.value}, ${scale_y.value});\n`
      } else return ''
    })

    watch(scaleCode, (newVal) => {
      ctx.emit('scaleEmit', {
        type: 'scale',
        code: newVal,
      })
    })

    const parseScaleProp = () => {
      if (props.scaleProp.transform) {
        const transform = props.scaleProp.transform
        const scaleMatch = transform.match(/scale\((\d+(\.\d+)?),\s*(\d+(\.\d+)?)\)/)
        if (scaleMatch) {
          scale_x.value = Number(scaleMatch[1])
          scale_y.value = Number(scaleMatch[3])
        }
      }
    }
    onMounted(() => {
      parseScaleProp()
    })
    const clearObjItem = () => {
      scale_x.value = ''
      scale_y.value = ''
      scalePreview.value.transform = ''
    }

    return {
      scalePreview,
      scaleCode,
      scale_x,
      scale_y,
      clearObjItem,
    }
  },

  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.scale-preview {
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
