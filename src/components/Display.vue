<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Display" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="display_display"
          :options="display_displays"
          label="Value"
          class="mb-10"
        />
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="preview" :style="displayPreview"></div>
      </div>
      <div class="code-box">{{ displayCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['displayEmit'],
  props: {
    displayProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const display_display = ref('')
    const display_displays = [
      '',
      'block',
      'none',
      'contents',
      'inline',
      'inline-block',
      'list-item',
      'table',
    ]
    const displayPreview = computed(() => {
      return {
        display: `${display_display.value}`,
      }
    })
    const displayCode = computed(() => {
      if (display_display.value) {
        return `display: ${display_display.value};\n`
      } else return ''
    })

    watch(displayCode, (newVal) => {
      ctx.emit('displayEmit', { type: 'display', code: newVal })
    })
    display_display.value = props.displayProp.display

    const clearObjItem = () => {
      display_display.value = ''
      displayPreview.value.display = ''
    }

    return {
      displayPreview,
      displayCode,
      display_display,
      display_displays,
      clearObjItem,
    }
  },

  components: {
    SubHeader,
  },
}
</script>

<style scoped></style>
