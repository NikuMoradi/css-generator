<template>
  <SubHeader title="Box Shadow" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="boxShadow_inset"
            :options="boxShadow_insets"
            label="Inset"
            class="mb-10"
          />
          <q-input label="Color" outlined v-model="boxShadow_color" class="mb-10">
            <template v-slot:append>
              <div
                class="show-color"
                :style="{
                  backgroundColor: boxShadow_color,
                }"
              ></div>
              <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                <q-color v-model="boxShadow_color" no-header-tabs :palette="colorPalette" />
              </q-popup-proxy>
            </template>
          </q-input>
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Horizontal offset</span><span>{{ boxShadow_horizontal_offset }} px</span>
            </div>
            <q-slider
              v-model="boxShadow_horizontal_offset"
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
              <span>Vertical offset</span><span>{{ boxShadow_vertical_offset }} px</span>
            </div>
            <q-slider
              v-model="boxShadow_vertical_offset"
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
              <span>‌Blur</span><span>{{ boxShadow_blur }} px</span>
            </div>
            <q-slider
              v-model="boxShadow_blur"
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
              <span>‌Spread</span><span>{{ boxShadow_spread }} px</span>
            </div>
            <q-slider
              v-model="boxShadow_spread"
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
        <div class="preview" :style="boxShadowPreview"></div>
      </div>
      <div class="code-box">{{ boxShadowCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['boxShadowEmit'],
  props: {
    boxShadowProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject('usedColors')

    const boxShadow_inset = ref('')
    const boxShadow_insets = ['Yes', 'No']
    const boxShadow_color = ref('')
    const boxShadow_horizontal_offset = ref()
    const boxShadow_vertical_offset = ref()
    const boxShadow_blur = ref()
    const boxShadow_spread = ref()
    const boxShadowPreview = computed(() => {
      if (boxShadow_inset.value == 'No') {
        return {
          boxShadow: `${boxShadow_horizontal_offset.value}px ${boxShadow_vertical_offset.value}px ${boxShadow_blur.value}px ${boxShadow_spread.value}px ${boxShadow_color.value}`,
        }
      } else {
        return {
          boxShadow: `${boxShadow_horizontal_offset.value}px ${boxShadow_vertical_offset.value}px ${boxShadow_blur.value}px ${boxShadow_spread.value}px ${boxShadow_color.value} inset`,
        }
      }
    })
    watch(boxShadow_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        boxShadow_color.value = ''
      }
    })
    const boxShadowCode = computed(() => {
      if (
        boxShadow_horizontal_offset.value !== undefined &&
        boxShadow_vertical_offset.value !== undefined &&
        boxShadow_blur.value !== undefined &&
        boxShadow_spread.value !== undefined &&
        boxShadow_horizontal_offset.value !== '' &&
        boxShadow_vertical_offset.value !== '' &&
        boxShadow_blur.value !== '' &&
        boxShadow_spread.value !== ''
      ) {
        if (boxShadow_inset.value === 'No') {
          return `box-shadow: ${boxShadow_horizontal_offset.value}px ${boxShadow_vertical_offset.value}px ${boxShadow_blur.value}px ${boxShadow_spread.value}px ${boxShadow_color.value};\n`
        } else {
          return `box-shadow: ${boxShadow_horizontal_offset.value}px ${boxShadow_vertical_offset.value}px ${boxShadow_blur.value}px ${boxShadow_spread.value}px ${boxShadow_color.value} inset;\n`
        }
      } else {
        return ''
      }
    })
    watch(boxShadowCode, (newValue) => {
      ctx.emit('boxShadowEmit', { type: 'boxShadow', code: newValue })
    })

    function parseBoxShadow(boxShadowValue) {
      if (boxShadowValue) {
        const regex =
          /(-?\d+px)\s+(-?\d+px)\s+(-?\d+px)\s+(-?\d+px)\s*(#\w{6}|rgba?\(\d+, \d+, \d+(, \d+(\.\d+)?)?\))?\s*(inset)?/
        const match = boxShadowValue.match(regex)

        if (match) {
          return {
            h_offset: Number(match[1].replace('px', '')),
            v_offset: Number(match[2].replace('px', '')),
            blur: Number(match[3].replace('px', '')),
            spread: Number(match[4].replace('px', '')),
            color: match[5] || '', // Handle optional color
            inset: match[8] ? 'Yes' : 'No', // Handle optional inset
          }
        }
        return null
      }
    }
    if (props.boxShadowProp) {
      const boxShadowValue = props.boxShadowProp['box-shadow']
      const parsedBoxShadow = parseBoxShadow(boxShadowValue)

      if (parsedBoxShadow) {
        const { h_offset, v_offset, blur, spread, color, inset } = parsedBoxShadow
        boxShadow_horizontal_offset.value = h_offset
        boxShadow_vertical_offset.value = v_offset
        boxShadow_blur.value = blur
        boxShadow_spread.value = spread
        boxShadow_color.value = color
        boxShadow_inset.value = inset
      }
    }

    const clearObjItem = () => {
      boxShadow_inset.value = ''
      boxShadow_color.value = ''
      boxShadow_horizontal_offset.value = ''
      boxShadow_vertical_offset.value = ''
      boxShadow_blur.value = ''
      boxShadow_spread.value = ''
      boxShadowPreview.value.boxShadow = ''
    }

    return {
      colorPalette,
      boxShadowPreview,
      boxShadowCode,
      boxShadow_inset,
      boxShadow_insets,
      boxShadow_color,
      boxShadow_horizontal_offset,
      boxShadow_vertical_offset,
      boxShadow_blur,
      boxShadow_spread,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped></style>
