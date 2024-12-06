<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Padding" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-md-6 col-sm-12 col-xs-12">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="padding_type"
            :options="padding_types"
            label="Type"
            class="mb-10"
          />
          <div
            v-if="padding_type == 'Same on all sides'"
            class="same-padding-items row q-col-gutter-sm q-my-lg"
          >
            <div class="col-6">
              <q-input
                v-model.number="padding"
                label="Value"
                type="number"
                outlined
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="padding_unitType"
                :options="padding_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <div class="different-padding-items" v-if="padding_type == 'Different on all sides'">
            <div class="row-wrapper">
              <p class="secondary-title">Top</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="padding_top"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="padding_top_unitType"
                    :options="padding_top_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Right</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="padding_right"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="padding_right_unitType"
                    :options="padding_right_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Bottom</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="padding_bottom"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="padding_bottom_unitType"
                    :options="padding_bottom_unitTypes"
                    label="Unit"
                    class="mb-10"
                  />
                </div>
              </div>
            </div>
            <div class="row-wrapper">
              <p class="secondary-title">Left</p>
              <div class="row q-col-gutter-x-sm">
                <div class="col-6">
                  <q-input
                    v-model.number="padding_left"
                    label="Value"
                    type="number"
                    outlined
                    class="mb-10"
                  />
                </div>
                <div class="col-6">
                  <q-select
                    outlined
                    v-model="padding_left_unitType"
                    :options="padding_left_unitTypes"
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
    <div class="col-md-5 col-sm-12 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="preview" :style="paddingPreview">
          <div class="padding-content">Content</div>
        </div>
      </div>
      <div class="code-box">{{ paddingCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['paddingEmit'],
  props: {
    paddingProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const padding_type = ref('Same on all sides')
    const padding_types = ['Same on all sides', 'Different on all sides']

    const padding = ref('')
    const padding_top = ref('')
    const padding_right = ref('')
    const padding_bottom = ref('')
    const padding_left = ref('')
    const padding_unitType = ref('')
    const padding_unitTypes = [
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
    const padding_top_unitType = ref('')
    const padding_top_unitTypes = [
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
    const padding_right_unitType = ref('')
    const padding_right_unitTypes = [
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
    const padding_bottom_unitType = ref('')
    const padding_bottom_unitTypes = [
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
    const padding_left_unitType = ref('')
    const padding_left_unitTypes = [
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
    const paddingPreview = computed(() => {
      if (padding_type.value == 'Same on all sides') {
        return {
          padding: `${padding.value}${padding_unitType.value}`,
        }
      } else {
        return {
          paddingTop: `${padding_top.value}${padding_top_unitType.value}`,
          paddingRight: `${padding_right.value}${padding_right_unitType.value}`,
          paddingBottom: `${padding_bottom.value}${padding_bottom_unitType.value}`,
          paddingLeft: `${padding_left.value}${padding_left_unitType.value}`,
        }
      }
    })

    const paddingCode = computed(() => {
      let code = ''

      if (padding_type.value == 'Same on all sides') {
        if (paddingPreview.value.padding && padding_unitType.value) {
          code += `padding: ${padding.value}${padding_unitType.value};\n`
        }
      } else {
        if (paddingPreview.value.paddingTop && padding_top_unitType.value) {
          code += `padding-top: ${padding_top.value}${padding_top_unitType.value};\n`
        }
        if (paddingPreview.value.paddingRight && padding_right_unitType.value) {
          code += `padding-right:${padding_right.value}${padding_right_unitType.value};\n`
        }
        if (paddingPreview.value.paddingBottom && padding_bottom_unitType.value) {
          code += `padding-bottom: ${padding_bottom.value}${padding_bottom_unitType.value};\n`
        }
        if (paddingPreview.value.paddingLeft && padding_left_unitType.value) {
          code += `padding-left: ${padding_left.value}${padding_left_unitType.value};\n`
        }
      }
      return code
    })
    watch(paddingCode, (newVal) => {
      ctx.emit('paddingEmit', { type: 'padding', code: newVal })
    })
    const extractValueAndUnit = (value) => {
      const match = value.match(/^(\d+)([a-z%]*)$/)
      return match ? [match[1], match[2]] : [value, '']
    }

    Object.entries(props.paddingProp).forEach(([key, value]) => {
      switch (key) {
        case 'padding': {
          const [paddingValue, unitType] = extractValueAndUnit(value)
          padding.value = paddingValue
          padding_unitType.value = unitType
          break
        }
        case 'padding-top': {
          const [paddingTopValue, topUnitType] = extractValueAndUnit(value)
          padding_top.value = paddingTopValue
          padding_top_unitType.value = topUnitType
          break
        }
        case 'padding-right': {
          const [paddingRightValue, rightUnitType] = extractValueAndUnit(value)
          padding_right.value = paddingRightValue
          padding_right_unitType.value = rightUnitType
          break
        }
        case 'padding-bottom': {
          const [paddingBottomValue, bottomUnitType] = extractValueAndUnit(value)
          padding_bottom.value = paddingBottomValue
          padding_bottom_unitType.value = bottomUnitType
          break
        }
        case 'padding-left': {
          const [paddingLeftValue, leftUnitType] = extractValueAndUnit(value)
          padding_left.value = paddingLeftValue
          padding_left_unitType.value = leftUnitType
          break
        }
      }
    })
    onMounted(() => {
      if (padding.value) {
        padding_type.value = 'Same on all sides'
      } else if (
        padding_top.value ||
        padding_right.value ||
        padding_bottom.value ||
        padding_left.value
      ) {
        padding_type.value = 'Different on all sides'
      }
    })
    const clearObjItem = () => {
      padding.value = ''
      padding_top.value = ''
      padding_right.value = ''
      padding_bottom.value = ''
      padding_left.value = ''
      padding_unitType.value = ''
      padding_top_unitType.value = ''
      padding_right_unitType.value = ''
      padding_bottom_unitType.value = ''
      padding_left_unitType.value = ''
    }

    return {
      paddingPreview,
      paddingCode,
      padding_type,
      padding_types,
      padding,
      padding_top,
      padding_right,
      padding_bottom,
      padding_left,
      padding_unitType,
      padding_unitTypes,
      padding_top_unitType,
      padding_top_unitTypes,
      padding_right_unitType,
      padding_right_unitTypes,
      padding_bottom_unitType,
      padding_bottom_unitTypes,
      padding_left_unitType,
      padding_left_unitTypes,
      clearObjItem,
    }
  },

  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.padding-content {
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
</style>
