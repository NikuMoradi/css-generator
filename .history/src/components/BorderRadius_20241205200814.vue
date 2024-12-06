<template>
  <SubHeader title="Border Radius" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-md-6 col-sm-12 col-xs-12">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="radius_type"
            :options="radius_types"
            label="Type"
            class="mb-10"
          />
          <div
            class="same-border-items row q-my-lg q-col-gutter-sm"
            v-if="radius_type == 'Same on all sides'"
          >
            <div class="col-6">
              <q-input
                v-model.number="radius_radius"
                label="Value"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="radius_unitType"
                :options="radius_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <div class="different-border-items" v-if="radius_type == 'Different on all sides'">
            <div class="row-wrapper">
              <p class="secondary-title">Top Left</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="radius_top_left"
                    label="Value"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="radius_top_left_unitType"
                    :options="radius_top_left_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>

            <div class="row-wrapper">
              <p class="secondary-title">Top Right</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="radius_top_right"
                    label="Value"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="radius_top_right_unitType"
                    :options="radius_top_right_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <div class="row-wrapper">
                <p class="secondary-title">Bottom Right</p>
                <div class="row q-col-gutter-x-sm">
                  <div class="col-6">
                    <q-input
                      v-model.number="radius_bottom_right"
                      label="Value"
                      type="number"
                      outlined
                      min="0"
                      class="mb-10"
                    />
                  </div>
                  <div class="col-6">
                    <q-select
                      outlined
                      v-model="radius_bottom_right_unitType"
                      :options="radius_bottom_right_unitTypes"
                      label="Unit"
                      class="mb-10"
                    />
                  </div>
                </div>
              </div>
              <p class="secondary-title">Bottom Left</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="radius_bottom_left"
                    label="Value"
                    type="number"
                    outlined
                    min="0"
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="radius_bottom_left_unitType"
                    :options="radius_bottom_left_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
          </div></div
      ></q-scroll-area>
    </div>
    <div class="col-md-5 col-sm-12 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="preview" :style="radiusPreview"></div>
      </div>
      <div class="code-box">{{ radiusCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['borderRadiusEmit'],
  props: {
    borderRadiusProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const radius_type = ref('Same on all sides')
    const radius_types = ['Same on all sides', 'Different on all sides']
    const radius_radius = ref('')
    const radius_top_left = ref('')
    const radius_top_right = ref('')
    const radius_bottom_right = ref('')
    const radius_bottom_left = ref('')
    const radius_unitType = ref('')
    const radius_unitTypes = [
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
    const radius_top_left_unitType = ref('')
    const radius_top_left_unitTypes = [
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
    const radius_top_right_unitType = ref('')
    const radius_top_right_unitTypes = [
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
    const radius_bottom_left_unitType = ref('')
    const radius_bottom_left_unitTypes = [
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
    const radius_bottom_right_unitType = ref('')
    const radius_bottom_right_unitTypes = [
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
    const radiusPreview = computed(() => {
      if (radius_type.value == 'Same on all sides') {
        return {
          borderRadius: `${radius_radius.value}${radius_unitType.value}`,
        }
      } else {
        return {
          borderTopLeftRadius: `${radius_top_left.value}${radius_top_left_unitType.value}`,
          borderTopRightRadius: `${radius_top_right.value}${radius_top_right_unitType.value}`,
          borderBottomRightRadius: `${radius_bottom_right.value}${radius_bottom_right_unitType.value}`,
          borderBottomLeftRadius: `${radius_bottom_left.value}${radius_bottom_left_unitType.value}`,
        }
      }
    })

    const isFilledRadius = computed(() => {
      return radius_radius.value !== '' && radius_unitType.value !== ''
    })

    const isFilledTopLeft = computed(() => {
      return radius_top_left.value !== '' && radius_top_left_unitType.value !== ''
    })

    const isFilledTopRight = computed(() => {
      return radius_top_right.value !== '' && radius_top_right_unitType.value !== ''
    })

    const isFilledBottomLeft = computed(() => {
      return radius_bottom_left.value !== '' && radius_bottom_left_unitType.value !== ''
    })

    const isFilledBottomRight = computed(() => {
      return radius_bottom_right.value !== '' && radius_bottom_right_unitType.value !== ''
    })

    const radiusCode = computed(() => {
      let code = ''

      if (radius_type.value === 'Same on all sides') {
        if (isFilledRadius.value) {
          code += `border-radius: ${radius_radius.value}${radius_unitType.value};\n`
        }
      } else {
        if (isFilledTopLeft.value) {
          code = ''
          code += `border-top-left-radius: ${radius_top_left.value}${radius_top_left_unitType.value};\n`
        }
        if (isFilledTopRight.value) {
          code += `border-top-right-radius: ${radius_top_right.value}${radius_top_right_unitType.value};\n`
        }
        if (isFilledBottomLeft.value) {
          code += `border-bottom-left-radius: ${radius_bottom_left.value}${radius_bottom_left_unitType.value};\n`
        }
        if (isFilledBottomRight.value) {
          code += `border-bottom-right-radius: ${radius_bottom_right.value}${radius_bottom_right_unitType.value};\n`
        }
      }

      return code
    })

    watch(radiusCode, (newValue) => {
      ctx.emit('borderRadiusEmit', { type: 'borderRadius', code: newValue })
    })
    function parseBorderRadiusValue(borderRadiusValue) {
      const regex = /(\d+(?:\.\d+)?)([a-zA-Z%]+)/
      const match = borderRadiusValue.match(regex)
      if (match) {
        return {
          radius: match[1],
          unit: match[2] || '',
        }
      }
      return null
    }
    const borderRadiusMap = {
      'border-radius': {
        radius: radius_radius,
        unit: radius_unitType,
      },
      'border-top-right-radius': {
        radius: radius_top_right,
        unit: radius_top_right_unitType,
      },
      'border-top-left-radius': {
        radius: radius_top_left,
        unit: radius_top_left_unitType,
      },
      'border-bottom-right-radius': {
        radius: radius_bottom_right,
        unit: radius_bottom_right_unitType,
      },
      'border-bottom-left-radius': {
        radius: radius_bottom_left,
        unit: radius_bottom_left_unitType,
      },
    }
    Object.entries(props.borderRadiusProp).forEach(([key, value]) => {
      const parsedBorderRadius = parseBorderRadiusValue(value)
      if (parsedBorderRadius && borderRadiusMap[key]) {
        const { radius, unit } = parsedBorderRadius
        borderRadiusMap[key].radius.value = radius
        borderRadiusMap[key].unit.value = unit
      }
    })
    onMounted(() => {
      if (isFilledRadius.value) {
        radius_type.value = 'Same on all sides'
      } else if (
        isFilledTopLeft.value ||
        isFilledTopRight.value ||
        isFilledBottomLeft.value ||
        isFilledBottomRight.value
      ) {
        radius_type.value = 'Different on all sides'
      }
    })
    const clearObjItem = () => {
      radius_radius.value = ''
      radius_top_left.value = ''
      radius_top_right.value = ''
      radius_bottom_right.value = ''
      radius_bottom_left.value = ''
      radius_unitType.value = ''
      radius_top_left_unitType.value = ''
      radius_top_right_unitType.value = ''
      radius_bottom_left_unitType.value = ''
      radius_bottom_right_unitType.value = ''
    }
    return {
      radiusCode,
      radiusPreview,
      radius_type,
      radius_types,
      radius_radius,
      radius_top_left,
      radius_top_right,
      radius_bottom_right,
      radius_bottom_left,
      radius_unitType,
      radius_unitTypes,
      radius_top_left_unitType,
      radius_top_left_unitTypes,
      radius_top_right_unitType,
      radius_top_right_unitTypes,
      radius_bottom_left_unitType,
      radius_bottom_left_unitTypes,
      radius_bottom_right_unitType,
      radius_bottom_right_unitTypes,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped></style>
