<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Border" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="border_type"
            :options="border_types"
            label="Type"
            class="mb-10"
          />
          <div
            v-if="border_type == 'Same on all sides'"
            class="same-border-items row q-col-gutter-sm q-my-lg"
          >
            <div class="col-xs-6 col-sm-3">
              <q-input label="Color" outlined v-model="border_color">
                <template v-slot:append>
                  <div class="show-color" :style="{ backgroundColor: border_color }"></div>
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-color v-model="border_color" no-header-tabs :palette="colorPalette" />
                  </q-popup-proxy>
                </template>
              </q-input>
            </div>
            <div class="col-xs-6 col-sm-3">
              <q-select
                outlined
                v-model="border_style"
                :options="border_styles"
                label="Style"
                class="mb-10"
              />
            </div>
            <div class="col-xs-6 col-sm-3">
              <q-input
                v-model.number="border_width"
                label="width"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-xs-6 col-sm-3">
              <q-select
                outlined
                v-model="border_unitType"
                :options="border_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <div class="different-border-items" v-if="border_type == 'Different on all sides'">
            <div class="row-wrapper">
              <p class="secondary-title">Top</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-xs-6 col-sm-3">
                  <q-input label="Color" outlined v-model="border_top_color">
                    <template v-slot:append>
                      <div class="show-color" :style="{ backgroundColor: border_top_color }"></div>
                      <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                        <q-color
                          v-model="border_top_color"
                          no-header-tabs
                          :palette="colorPalette"
                        />
                      </q-popup-proxy>
                    </template>
                  </q-input>
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_top_style"
                    :options="border_top_styles"
                    label="Style"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-input
                    v-model.number="border_top_width"
                    label="width"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_top_unitType"
                    :options="border_top_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Right</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-xs-6 col-sm-3">
                  <q-input label="Color" outlined v-model="border_right_color">
                    <template v-slot:append>
                      <div
                        class="show-color"
                        :style="{
                          backgroundColor: border_right_color,
                        }"
                      ></div>
                      <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                        <q-color
                          v-model="border_right_color"
                          no-header-tabs
                          :palette="colorPalette"
                        />
                      </q-popup-proxy>
                    </template>
                  </q-input>
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_right_style"
                    :options="border_right_styles"
                    label="Style"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-input
                    v-model.number="border_right_width"
                    label="width"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_right_unitType"
                    :options="border_right_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Bottom</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-xs-6 col-sm-3">
                  <q-input label="Color" outlined v-model="border_bottom_color">
                    <template v-slot:append>
                      <div
                        class="show-color"
                        :style="{
                          backgroundColor: border_bottom_color,
                        }"
                      ></div>
                      <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                        <q-color
                          v-model="border_bottom_color"
                          no-header-tabs
                          :palette="colorPalette"
                        />
                      </q-popup-proxy>
                    </template>
                  </q-input>
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_bottom_style"
                    :options="border_bottom_styles"
                    label="Style"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-input
                    v-model.number="border_bottom_width"
                    label="width"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_bottom_unitType"
                    :options="border_bottom_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Left</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-xs-6 col-sm-3">
                  <q-input label="Color" outlined v-model="border_left_color">
                    <template v-slot:append>
                      <div
                        class="show-color"
                        :style="{
                          backgroundColor: border_left_color,
                        }"
                      ></div>
                      <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                        <q-color
                          v-model="border_left_color"
                          no-header-tabs
                          :palette="colorPalette"
                        />
                      </q-popup-proxy>
                    </template>
                  </q-input>
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_left_style"
                    :options="border_left_styles"
                    label="Style"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-input
                    v-model.number="border_left_width"
                    label="width"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-xs-6 col-sm-3">
                  <q-select
                    outlined
                    v-model="border_left_unitType"
                    :options="border_left_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </q-scroll-area>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="preview" :style="borderPreview"></div>
      </div>
      <div class="code-box">{{ borderCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['borderEmit'],
  props: {
    borderProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject('usedColors')
    const border_type = ref('Same on all sides')
    const border_types = ['Same on all sides', 'Different on all sides']
    const border_color = ref('')
    const border_top_color = ref('')
    const border_right_color = ref('')
    const border_bottom_color = ref('')
    const border_left_color = ref('')

    const border_style = ref('')
    const border_styles = ['', 'dotted', 'dashed', 'solid', 'double', 'groove', 'ridge', 'inset']
    const border_top_style = ref('')
    const border_top_styles = [
      '',
      'dotted',
      'dashed',
      'solid',
      'double',
      'groove',
      'ridge',
      'inset',
      'outset',
    ]
    const border_right_style = ref('')
    const border_right_styles = [
      '',
      'dotted',
      'dashed',
      'solid',
      'double',
      'groove',
      'ridge',
      'inset',
      'outset',
    ]
    const border_bottom_style = ref('')
    const border_bottom_styles = [
      '',
      'dotted',
      'dashed',
      'solid',
      'double',
      'groove',
      'ridge',
      'inset',
      'outset',
    ]
    const border_left_style = ref('')
    const border_left_styles = [
      '',
      'dotted',
      'dashed',
      'solid',
      'double',
      'groove',
      'ridge',
      'inset',
      'outset',
    ]

    const border_width = ref('')
    const border_top_width = ref('')
    const border_right_width = ref('')
    const border_bottom_width = ref('')
    const border_left_width = ref('')

    const border_unitType = ref('')
    const border_unitTypes = [
      '',
      'px', // Pixels are the most basic unit and are used to define fixed sizes[^1^][3].
      '%', // Percentages are used to define sizes relative to parent elements[^1^][3].
      'em', // Ems are used to define sizes relative to the font size of the parent element[^1^][3].
      'rem', // Rems are similar to ems but are relative to the root element's font size[^1^][3].
      'vw', // Viewport width units are relative to 1% of the width of the viewport[^1^][3].
      'vh', // Viewport height units are relative to 1% of the height of the viewport[^1^][3].
      'vmin', // Viewport minimum units are relative to the smaller dimension of the viewport[^1^][3].
      'vmax', // Viewport maximum units are relative to the larger dimension of the viewport[^1^][3].
      'cm', // Centimeters are absolute units and are not commonly used for screen styles[^2^][2].
      'mm', // Millimeters are also absolute units and are less common for screen styles[^2^][2].
      'pt', // Points are often used in print but can be used for screen styles as well[^2^][2].
      'pc', // Picas are similar to points and are not commonly used in modern web design[^2^][2].
      'ex', // Ex units are based on the x-height of the font and are not frequently used[^2^][2].
      'ch', // Character units are based on the width of the "0" character and are less common[^2^][2].
      'in',
    ]
    const border_top_unitType = ref('')
    const border_top_unitTypes = [
      '',
      'px',
      '%',
      'em',
      'rem',
      'vw',
      'vh',
      'vmin',
      'vmax',
      'cm',
      'mm',
      'pt',
      'pc',
      'ex',
      'ch',
      'in',
    ]
    const border_right_unitType = ref('')
    const border_right_unitTypes = [
      '',
      'px',
      '%',
      'em',
      'rem',
      'vw',
      'vh',
      'vmin',
      'vmax',
      'cm',
      'mm',
      'pt',
      'pc',
      'ex',
      'ch',
      'in',
    ]
    const border_bottom_unitType = ref('')
    const border_bottom_unitTypes = [
      '',
      'px',
      '%',
      'em',
      'rem',
      'vw',
      'vh',
      'vmin',
      'vmax',
      'cm',
      'mm',
      'pt',
      'pc',
      'ex',
      'ch',
      'in',
    ]
    const border_left_unitType = ref('')
    const border_left_unitTypes = [
      '',
      'px',
      '%',
      'em',
      'rem',
      'vw',
      'vh',
      'vmin',
      'vmax',
      'cm',
      'mm',
      'pt',
      'pc',
      'ex',
      'ch',
      'in',
    ]
    watch(border_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        border_color.value = ''
      }
    })
    watch(border_top_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        border_top_color.value = ''
      }
    })
    watch(border_right_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        border_right_color.value = ''
      }
    })
    watch(border_bottom_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        border_bottom_color.value = ''
      }
    })
    watch(border_left_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        border_left_color.value = ''
      }
    })

    const isFilledBorder = computed(() => {
      return border_width.value && border_unitType.value && border_style.value && border_color.value
    })
    const isFilledBorderTop = computed(() => {
      return (
        border_top_width.value &&
        border_top_unitType.value &&
        border_top_style.value &&
        border_top_color.value
      )
    })
    const isFilledBorderRight = computed(() => {
      return (
        border_right_width.value &&
        border_right_unitType.value &&
        border_right_style.value &&
        border_right_color.value
      )
    })
    const isFilledBorderBottom = computed(() => {
      return (
        border_bottom_width.value &&
        border_bottom_unitType.value &&
        border_bottom_style.value &&
        border_bottom_color.value
      )
    })
    const isFilledBorderLeft = computed(() => {
      return (
        border_left_width.value &&
        border_left_unitType.value &&
        border_left_style.value &&
        border_left_color.value
      )
    })
    const borderPreview = computed(() => {
      if (border_type.value == 'Same on all sides') {
        return {
          border: `${border_width.value}${border_unitType.value} ${border_style.value} ${border_color.value}`,
        }
      } else {
        return {
          borderTop: `${border_top_width.value}${border_top_unitType.value} ${border_top_style.value} ${border_top_color.value}`,
          borderRight: `${border_right_width.value}${border_right_unitType.value} ${border_right_style.value} ${border_right_color.value}`,
          borderBottom: `${border_bottom_width.value}${border_bottom_unitType.value} ${border_bottom_style.value} ${border_bottom_color.value}`,
          borderLeft: `${border_left_width.value}${border_left_unitType.value} ${border_left_style.value} ${border_left_color.value}`,
        }
      }
    })

    const borderCode = computed(() => {
      let code = ''

      if (border_type.value === 'Same on all sides') {
        if (isFilledBorder.value) {
          code = ''
          code += `border: ${border_width.value}${border_unitType.value} ${border_style.value} ${border_color.value};\n`
        }
      } else {
        if (isFilledBorderTop.value) {
          code += `border-top: ${border_top_width.value}${border_top_unitType.value} ${border_top_style.value} ${border_top_color.value};\n`
        }
        if (isFilledBorderRight.value) {
          code += `border-right: ${border_right_width.value}${border_right_unitType.value} ${border_right_style.value} ${border_right_color.value};\n`
        }
        if (isFilledBorderBottom.value) {
          code += `border-bottom: ${border_bottom_width.value}${border_bottom_unitType.value} ${border_bottom_style.value} ${border_bottom_color.value};\n`
        }
        if (isFilledBorderLeft.value) {
          code += `border-left: ${border_left_width.value}${border_left_unitType.value} ${border_left_style.value} ${border_left_color.value};\n`
        }
      }

      return code
    })
    watch(borderCode, (newValue) => {
      ctx.emit('borderEmit', { type: 'border', code: newValue })
    })

    function parseBorderValue(borderValue) {
      const regex = /(\d+(?:\.\d+)?)([a-zA-Z%]+)?\s(\w+)\s(#\w{6}|\w+)/
      const match = borderValue.match(regex)
      if (match) {
        return {
          width: match[1],
          unit: match[2] || '',
          style: match[3],
          color: match[4],
        }
      }

      return null
    }

    const borderMap = {
      border: {
        width: border_width,
        unit: border_unitType,
        style: border_style,
        color: border_color,
      },
      'border-top': {
        width: border_top_width,
        unit: border_top_unitType,
        style: border_top_style,
        color: border_top_color,
      },
      'border-right': {
        width: border_right_width,
        unit: border_right_unitType,
        style: border_right_style,
        color: border_right_color,
      },
      'border-bottom': {
        width: border_bottom_width,
        unit: border_bottom_unitType,
        style: border_bottom_style,
        color: border_bottom_color,
      },
      'border-left': {
        width: border_left_width,
        unit: border_left_unitType,
        style: border_left_style,
        color: border_left_color,
      },
    }

    Object.entries(props.borderProp).forEach(([key, value]) => {
      const parsedBorder = parseBorderValue(value)

      if (parsedBorder && borderMap[key]) {
        const { width, unit, style, color } = parsedBorder
        borderMap[key].width.value = width
        borderMap[key].unit.value = unit
        borderMap[key].style.value = style
        borderMap[key].color.value = color
      }
    })
    onMounted(() => {
      if (isFilledBorder.value) {
        border_type.value = 'Same on all sides'
      } else if (
        isFilledBorderTop.value ||
        isFilledBorderBottom.value ||
        isFilledBorderRight.value ||
        isFilledBorderLeft.value
      ) {
        border_type.value = 'Different on all sides'
      }
    })
    const clearObjItem = () => {
      border_color.value = ''
      border_style.value = ''
      border_width.value = ''
      border_top_color.value = ''
      border_right_color.value = ''
      border_bottom_color.value = ''
      border_left_color.value = ''
      border_top_style.value = ''
      border_right_style.value = ''
      border_bottom_style.value = ''
      border_left_style.value = ''
      border_top_width.value = ''
      border_right_width.value = ''
      border_bottom_width.value = ''
      border_left_width.value = ''
      border_unitType.value = ''
      border_top_unitType.value = ''
      border_right_unitType.value = ''
      border_bottom_unitType.value = ''
      border_left_unitType.value = ''
      borderPreview.value.border = ''
      borderPreview.value.borderTop = ''
      borderPreview.value.borderRight = ''
      borderPreview.value.borderBottom = ''
      borderPreview.value.borderLeft = ''
    }

    return {
      colorPalette,
      borderPreview,
      borderCode,
      border_type,
      border_types,
      border_color,
      border_style,
      border_styles,
      border_width,
      border_top_color,
      border_right_color,
      border_bottom_color,
      border_left_color,
      border_top_style,
      border_top_styles,
      border_right_style,
      border_right_styles,
      border_bottom_style,
      border_bottom_styles,
      border_left_style,
      border_left_styles,
      border_top_width,
      border_right_width,
      border_bottom_width,
      border_left_width,
      border_unitType,
      border_unitTypes,
      border_top_unitType,
      border_top_unitTypes,
      border_right_unitType,
      border_right_unitTypes,
      border_bottom_unitType,
      border_bottom_unitTypes,
      border_left_unitType,
      border_left_unitTypes,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped></style>
