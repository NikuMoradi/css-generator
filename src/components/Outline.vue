<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Outline" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-input label="Color" outlined v-model="outline_color" class="mb-10">
          <template v-slot:append>
            <div
              class="show-color"
              :style="{
                backgroundColor: outline_color,
              }"
            ></div>
            <q-popup-proxy cover transition-show="scale" transition-hide="scale">
              <q-color v-model="outline_color" no-header-tabs :palette="colorPalette" />
            </q-popup-proxy>
          </template>
        </q-input>
        <q-select
          outlined
          v-model="outline_style"
          :options="outline_styles"
          label="Style"
          class="mb-10"
        />
        <div class="row q-col-gutter-x-sm mb-10">
          <div class="col-6">
            <q-input v-model.number="outline_width" label="Width" type="number" outlined min="0" />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="outline_width_unitType"
              :options="outline_width_unitTypes"
              label="Unit"
            />
          </div>
        </div>

        <div class="row q-col-gutter-x-sm q-my-lg">
          <div class="col-xs-6 col-sm-6">
            <q-input v-model.number="outline_offset" label="Offset" type="number" outlined />
          </div>
          <div class="col-xs-6 col-sm-6">
            <q-select
              outlined
              v-model="outline_offset_unitType"
              :options="outline_offset_unitTypes"
              label="Unit"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="preview" :style="outlinePreview"></div>
      </div>
      <div class="code-box">{{ outlineCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['outlineEmit'],
  props: {
    outlineProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject('usedColors')

    const outline_color = ref('')
    const outline_style = ref('')
    const outline_styles = ['', 'dotted', 'dashed', 'solid', 'double', 'groove', 'ridge']
    const outline_width = ref('')
    const outline_offset = ref('')
    const outline_width_unitType = ref('')
    const outline_width_unitTypes = [
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
    const outline_offset_unitType = ref('')
    const outline_offset_unitTypes = [
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
    watch(outline_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        outline_color.value = '' // Reset to default color if invalid
      }
    })
    const outlinePreview = computed(() => {
      return {
        outline: `${outline_width.value}${outline_width_unitType.value} ${outline_style.value} ${outline_color.value}`,
        outlineOffset: `${outline_offset.value}${outline_offset_unitType.value}`,
      }
    })

    const outlineCode = computed(() => {
      let code = ''
      if (outline_style.value && outline_width.value && outline_width_unitType.value) {
        code += `outline: ${outline_width.value}${outline_width_unitType.value} ${outline_style.value} ${outline_color.value};\n`
      }
      if (outline_offset.value && outline_offset_unitType.value) {
        code += `outline-offset: ${outline_offset.value}${outline_offset_unitType.value};\n`
      }
      return code
    })

    watch(outlineCode, (newVal) => {
      ctx.emit('outlineEmit', {
        type: 'outline',
        code: newVal,
      })
    })
    Object.entries(props.outlineProp).forEach(([key, value]) => {
      switch (key) {
        case 'outline': {
          const outlineMatch = value.match(/(-?\d+\.?\d*)([a-zA-Z%]*)\s+(\w+)\s+(.+)/)
          if (outlineMatch) {
            outline_width.value = outlineMatch[1]
            outline_width_unitType.value = outlineMatch[2]
            outline_style.value = outlineMatch[3]
            outline_color.value = outlineMatch[4]
          }
          break
        }
        case 'outline-offset': {
          const outlineOffsetMatch = value.match(/(-?\d+\.?\d*)([a-zA-Z%]*)/)
          if (outlineOffsetMatch) {
            outline_offset.value = outlineOffsetMatch[1]
            outline_offset_unitType.value = outlineOffsetMatch[2]
          }
          break
        }

        default:
          break
      }
    })

    const clearObjItem = () => {
      outline_color.value = ''
      outline_style.value = ''
      outline_width.value = ''
      outline_offset.value = ''
      outline_width_unitType.value = ''
      outline_offset_unitType.value = ''
      outlinePreview.value.outline = ''
      outlinePreview.value.outlineOffset = ''
    }

    return {
      colorPalette,
      outlinePreview,
      outlineCode,
      outline_color,
      outline_style,
      outline_styles,
      outline_width,
      outline_offset,
      outline_width_unitType,
      outline_width_unitTypes,
      outline_offset_unitType,
      outline_offset_unitTypes,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>
