<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Margin" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-md-6 col-sm-12 col-xs-12">
      <q-scroll-area style="height: 65vh">
        <div style="margin: 0 1rem">
          <q-select
            outlined
            v-model="margin_type"
            :options="margin_types"
            label="Type"
            class="mb-10"
          />
          <div v-if="margin_type == 'Same on all sides'" class="same-margin-items">
            <div class="title-auto-wrapper">
              <p class="secondary-title">All sides</p>
              <q-checkbox size="sm" v-model="margin_auto" val="auto" label="Auto" />
            </div>

            <div class="row q-col-gutter-sm mb-10">
              <div class="col-xs-6 col-md-6" v-if="!margin_auto">
                <q-input
                  v-model.number="margin"
                  label="Value"
                  type="number"
                  outlined
                  class="mb-10"
                />
              </div>
              <div class="col-xs-6 col-md-6" v-if="!margin_auto">
                <q-select
                  outlined
                  v-model="margin_unitType"
                  :options="margin_unitTypes"
                  label="Unit"
                  class="mb-10"
                />
              </div>
            </div>
          </div>
          <div class="different-margin-items" v-if="margin_type == 'Different on all sides'">
            <div class="wrapper mb-10">
              <div class="title-auto-wrapper">
                <p class="secondary-title">Top</p>
                <q-checkbox size="sm" v-model="margin_top_auto" val="auto" label="Auto" />
              </div>

              <div class="row q-col-gutter-x-sm">
                <div class="col-6" v-if="!margin_top_auto">
                  <q-input
                    v-model.number="margin_top"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6" v-if="!margin_top_auto">
                  <q-select
                    outlined
                    v-model="margin_top_unitType"
                    :options="margin_top_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="wrapper mb-10">
              <div class="title-auto-wrapper">
                <p class="secondary-title">Right</p>
                <q-checkbox size="sm" v-model="margin_right_auto" val="auto" label="Auto" />
              </div>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6" v-if="!margin_right_auto">
                  <q-input
                    v-model.number="margin_right"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6" v-if="!margin_right_auto">
                  <q-select
                    outlined
                    v-model="margin_right_unitType"
                    :options="margin_right_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="wrapper mb-10">
              <div class="title-auto-wrapper">
                <p class="secondary-title">Bottom</p>
                <q-checkbox size="sm" v-model="margin_bottom_auto" val="auto" label="Auto" />
              </div>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6" v-if="!margin_bottom_auto">
                  <q-input
                    v-model.number="margin_bottom"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6" v-if="!margin_bottom_auto">
                  <q-select
                    outlined
                    v-model="margin_bottom_unitType"
                    :options="margin_bottom_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="wrapper mb-10">
              <div class="title-auto-wrapper">
                <p class="secondary-title">Left</p>
                <q-checkbox size="sm" v-model="margin_left_auto" val="auto" label="Auto" />
              </div>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6" v-if="!margin_left_auto">
                  <q-input
                    v-model.number="margin_left"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6" v-if="!margin_left_auto">
                  <q-select
                    outlined
                    v-model="margin_left_unitType"
                    :options="margin_left_unitTypes"
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
    <div class="col-md-5 col-xs-12 q-gutter-y-lg">
      <div class="preview-box">
        <div class="preview" :style="marginPreview">
          <div class="margin-content">Content</div>
        </div>
      </div>
      <div class="code-box">{{ marginCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['marginEmit'],
  props: {
    marginProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const margin_type = ref('Same on all sides')
    const margin_types = ['Same on all sides', 'Different on all sides']
    const margin = ref('')
    const margin_top = ref('')
    const margin_right = ref('')
    const margin_bottom = ref('')
    const margin_left = ref('')
    const margin_unitType = ref('')
    const margin_unitTypes = [
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
    const margin_top_unitType = ref('')
    const margin_top_unitTypes = [
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
    const margin_right_unitType = ref('')
    const margin_right_unitTypes = [
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
    const margin_bottom_unitType = ref('')
    const margin_bottom_unitTypes = [
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
    const margin_left_unitType = ref('')
    const margin_left_unitTypes = [
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
    const margin_auto = ref(false)
    const margin_top_auto = ref(false)
    const margin_right_auto = ref(false)
    const margin_bottom_auto = ref(false)
    const margin_left_auto = ref(false)
    const marginPreview = computed(() => {
      if (margin_type.value == 'Same on all sides') {
        return {
          margin: !margin_auto.value ? `${margin.value}${margin_unitType.value}` : `auto`,
        }
      } else {
        return {
          marginTop: !margin_top_auto.value
            ? `${margin_top.value}${margin_top_unitType.value}`
            : `auto`,
          marginRight: !margin_right_auto.value
            ? `${margin_right.value}${margin_right_unitType.value}`
            : `auto`,
          marginBottom: !margin_bottom_auto.value
            ? `${margin_bottom.value}${margin_bottom_unitType.value}`
            : `auto`,
          marginLeft: !margin_left_auto.value
            ? `${margin_left.value}${margin_left_unitType.value}`
            : `auto`,
        }
      }
    })
    const marginCode = computed(() => {
      let code = ''
      if (margin_type.value == 'Same on all sides') {
        if ((margin.value && margin_unitType.value) || marginPreview.value.margin === 'auto') {
          code += `margin: ${marginPreview.value.margin};\n`
        }
      } else {
        if (
          (margin_top.value && margin_top_unitType.value) ||
          marginPreview.value.marginTop === 'auto'
        ) {
          code += `margin-top: ${marginPreview.value.marginTop};\n`
        }
        if (
          (margin_right.value && margin_right_unitType.value) ||
          marginPreview.value.marginRight === 'auto'
        ) {
          code += `margin-right: ${marginPreview.value.marginRight};\n`
        }
        if (
          (margin_bottom.value && margin_bottom_unitType.value) ||
          marginPreview.value.marginBottom === 'auto'
        ) {
          code += `margin-bottom: ${marginPreview.value.marginBottom};\n`
        }
        if (
          (margin_left.value && margin_left_unitType.value) ||
          marginPreview.value.marginLeft === 'auto'
        ) {
          code += `margin-left: ${marginPreview.value.marginLeft};\n`
        }
      }
      return code
    })

    watch(marginCode, (newVal) => {
      ctx.emit('marginEmit', { type: 'margin', code: newVal })
    })
    const extractValueAndUnit = (value) => {
      if (value === 'auto') {
        return ['auto', '']
      }
      const match = value.match(/^(\d+)([a-z%]*)$/)
      return match ? [match[1], match[2]] : [value, '']
    }

    Object.entries(props.marginProp).forEach(([key, value]) => {
      switch (key) {
        case 'margin':
          if (value === 'auto') {
            margin_auto.value = true
          } else {
            const [marginValue, unitType] = extractValueAndUnit(value)
            margin.value = marginValue
            margin_unitType.value = unitType
            margin_auto.value = false
          }
          break
        case 'margin-top':
          if (value === 'auto') {
            margin_top_auto.value = true
          } else {
            const [marginTopValue, unitType] = extractValueAndUnit(value)
            margin_top.value = marginTopValue
            margin_top_unitType.value = unitType
            margin_top_auto.value = false
          }
          break
        case 'margin-right':
          if (value === 'auto') {
            margin_right_auto.value = true
          } else {
            const [marginRightValue, unitType] = extractValueAndUnit(value)
            margin_right.value = marginRightValue
            margin_right_unitType.value = unitType
            margin_right_auto.value = false
          }
          break
        case 'margin-bottom':
          if (value === 'auto') {
            margin_bottom_auto.value = true
          } else {
            const [marginBottomValue, unitType] = extractValueAndUnit(value)
            margin_bottom.value = marginBottomValue
            margin_bottom_unitType.value = unitType
            margin_bottom_auto.value = false
          }
          break
        case 'margin-left':
          if (value === 'auto') {
            margin_left_auto.value = true
          } else {
            const [marginLeftValue, unitType] = extractValueAndUnit(value)
            margin_left.value = marginLeftValue
            margin_left_unitType.value = unitType
            margin_left_auto.value = false
          }
          break
      }
    })
    onMounted(() => {
      if (margin.value) {
        margin_type.value = 'Same on all sides'
      } else if (
        margin_top.value ||
        margin_right.value ||
        margin_bottom.value ||
        margin_left.value
      ) {
        margin_type.value = 'Different on all sides'
      }
    })
    const clearObjItem = () => {
      margin.value = ''
      margin_top.value = ''
      margin_right.value = ''
      margin_bottom.value = ''
      margin_left.value = ''
      margin_unitType.value = ''
      margin_top_unitType.value = ''
      margin_right_unitType.value = ''
      margin_bottom_unitType.value = ''
      margin_left_unitType.value = ''
      margin_auto.value = ''
      margin_top_auto.value = ''
      margin_right_auto.value = ''
      margin_bottom_auto.value = ''
      margin_left_auto.value = ''
    }

    return {
      marginPreview,
      marginCode,
      margin_type,
      margin_types,
      margin,
      margin_top,
      margin_right,
      margin_bottom,
      margin_left,
      margin_unitType,
      margin_unitTypes,
      margin_top_unitType,
      margin_top_unitTypes,
      margin_right_unitType,
      margin_right_unitTypes,
      margin_bottom_unitType,
      margin_bottom_unitTypes,
      margin_left_unitType,
      margin_left_unitTypes,
      margin_auto,
      margin_top_auto,
      margin_right_auto,
      margin_bottom_auto,
      margin_left_auto,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.margin-content {
  background-color: #ffffff;
  width: 50%;
  height: 50%;
  min-width: 4rem;
  min-height: 4rem;
  border-radius: 10px;
  font-size: 0.8rem;
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
}

.title-auto-wrapper {
  display: flex;
  justify-content: flex-start;
}
.outlined-checkbox {
  height: 3.48rem;
  padding: 0.6rem 0rem 0 0.5rem;
  border: 1px solid #ccc;
  color: #666;
  font-size: 0.7rem;
  border-radius: 4px;
  transition: 300ms;
}
.outlined-checkbox:hover {
  border-color: black;
}
.checkbox-label {
  line-height: 0.8;
}
</style>
