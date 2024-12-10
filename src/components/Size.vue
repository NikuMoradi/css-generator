<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Size" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="row q-col-gutter-sm">
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_width"
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
              v-model="size_width_unitType"
              :options="size_width_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_height"
              label="Height"
              type="number"
              outlined
              min="0"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-select
              outlined
              v-model="size_height_unitType"
              :options="size_height_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_min_width"
              label="Min Width"
              type="number"
              outlined
              min="0"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-select
              outlined
              v-model="size_min_width_unitType"
              :options="size_min_width_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_min_height"
              label="Min Height"
              type="number"
              outlined
              min="0"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-select
              outlined
              v-model="size_min_height_unitType"
              :options="size_min_height_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_max_width"
              label="Max Width"
              type="number"
              outlined
              min="0"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-select
              outlined
              v-model="size_max_width_unitType"
              :options="size_max_width_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-input
              v-model.number="size_max_height"
              label="Max Height"
              type="number"
              outlined
              min="0"
              class="mb-10"
            />
          </div>
          <div class="col-xs-6 col-sm-3">
            <q-select
              outlined
              v-model="size_max_height_unitType"
              :options="size_max_height_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="size-preview" :style="sizePreview"></div>
      </div>
      <div class="code-box">
        <q-scroll-area style="height: 4rem">
          {{ sizeCode }}
        </q-scroll-area>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['sizeEmit'],
  props: {
    sizeProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const unitType = ref('')
    const size_width = ref('')
    const size_height = ref('')
    const size_min_width = ref('')
    const size_min_height = ref('')
    const size_max_width = ref('')
    const size_max_height = ref('')
    const size_width_unitType = ref('')
    const size_width_unitTypes = [
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
    const size_height_unitType = ref('')
    const size_height_unitTypes = [
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
    const size_min_width_unitType = ref('')
    const size_min_width_unitTypes = [
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
    const size_min_height_unitType = ref('')
    const size_min_height_unitTypes = [
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
    const size_max_width_unitType = ref('')
    const size_max_width_unitTypes = [
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
    const size_max_height_unitType = ref('')
    const size_max_height_unitTypes = [
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
    const sizePreview = computed(() => {
      return {
        width: `${size_width.value}${size_width_unitType.value}`,
        height: `${size_height.value}${size_height_unitType.value}`,
        minWidth: `${size_min_width.value}${size_min_width_unitType.value}`,
        maxWidth: `${size_max_width.value}${unitType.value}`,
        minHeight: `${size_min_height.value}${size_max_width_unitType.value}`,
        maxHeight: `${size_max_height.value}${size_max_height_unitType.value}`,
      }
    })
    const sizeCode = computed(() => {
      let code = ''
      if (size_width.value !== '' && size_width_unitType.value !== '') {
        code += `width: ${size_width.value}${size_width_unitType.value};\n`
      }
      if (size_height.value !== '' && size_height_unitType.value !== '') {
        code += `height: ${size_height.value}${size_height_unitType.value};\n`
      }
      if (size_min_width.value !== '' && size_min_width_unitType.value !== '') {
        code += `min-width: ${size_min_width.value}${size_min_width_unitType.value};\n`
      }
      if (size_min_height.value !== '' && size_min_height_unitType.value !== '') {
        code += `min-height: ${size_min_height.value}${size_min_height_unitType.value};\n`
      }
      if (size_max_width.value !== '' && size_max_width_unitType.value !== '') {
        code += `max-width: ${size_max_width.value}${size_max_width_unitType.value};\n`
      }
      if (size_max_height.value !== '' && size_max_height_unitType.value !== '') {
        code += `max-height: ${size_max_height.value}${size_max_height_unitType.value};\n`
      }
      return code
    })
    watch(sizeCode, (newVal) => {
      ctx.emit('sizeEmit', { type: 'size', code: newVal })
    })

    const extractValueAndUnit = (value) => {
      const match = value.match(/^(\d+)([a-z%]*)$/)
      return match ? [match[1], match[2]] : ['', '']
    }

    // Parsing function
    Object.entries(props.sizeProp).forEach(([key, value]) => {
      const [numberValue, unitType] = extractValueAndUnit(value)

      switch (key) {
        case 'width':
          size_width.value = numberValue
          size_width_unitType.value = unitType
          break
        case 'height':
          size_height.value = numberValue
          size_height_unitType.value = unitType
          break
        case 'min-width':
          size_min_width.value = numberValue
          size_min_width_unitType.value = unitType
          break
        case 'min-height':
          size_min_height.value = numberValue
          size_min_height_unitType.value = unitType
          break
        case 'max-width':
          size_max_width.value = numberValue
          size_max_width_unitType.value = unitType
          break
        case 'max-height':
          size_max_height.value = numberValue
          size_max_height_unitType.value = unitType
          break
      }
    })

    const clearObjItem = () => {
      size_width.value = ''
      size_height.value = ''
      size_min_width.value = ''
      size_min_height.value = ''
      size_max_width.value = ''
      size_max_height.value = ''
      size_width_unitType.value = ''
      size_height_unitType.value = ''
      size_min_width_unitType.value = ''
      size_min_height_unitType.value = ''
      size_max_width_unitType.value = ''
      size_max_height_unitType.value = ''
    }

    return {
      sizePreview,
      sizeCode,
      size_width,
      size_height,
      size_min_width,
      size_min_height,
      size_max_width,
      size_max_height,
      size_width_unitType,
      size_width_unitTypes,
      size_height_unitType,
      size_height_unitTypes,
      size_min_width_unitType,
      size_min_width_unitTypes,
      size_min_height_unitType,
      size_min_height_unitTypes,
      size_max_width_unitType,
      size_max_width_unitTypes,
      size_max_height_unitType,
      size_max_height_unitTypes,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.size-preview {
  background-color: #ffffff;
  width: 19rem;
  height: 16rem;
  border: 2px solid #1976d239;
  font-size: 1rem;
  line-height: 1.9;
  padding: 0.8rem;
  white-space: nowrap;
  overflow: hidden;
}
</style>
