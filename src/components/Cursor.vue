<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Cursor" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="cursor_cursor"
          :options="cursor_cursors"
          label="Value"
          class="mb-10"
        />
      </div>
    </div>

    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="preview" :style="cursorPreview">
          Mouse over this area to see the cursor result.
        </div>
      </div>
      <div class="code-box">{{ cursorCode }}</div>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue'
import SubHeader from './SubHeader.vue'
export default {
  emits: ['cursorEmit'],
  props: {
    cursorProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const cursor_cursor = ref('') // Initial value
    const cursor_cursors = [
      '',
      'auto',
      'default',
      'none',
      'context-menu',
      'help',
      'pointer',
      'progress',
      'wait',
      'cell',
      'crosshair',
      'text',
      'vertical-text',
      'alias',
      'copy',
      'move',
      'no-drop',
      'not-allowed',
      'grab',
      'grabbing',
      'all-scroll',
      'col-resize',
      'row-resize',
      'n-resize',
      'e-resize',
      's-resize',
      'w-resize',
      'ne-resize',
      'nw-resize',
      'se-resize',
      'sw-resize',
      'ew-resize',
      'ns-resize',
      'nesw-resize',
      'nwse-resize',
      'zoom-in',
      'zoom-out',
    ]
    const cursorPreview = computed(() => {
      return {
        cursor: `${cursor_cursor.value}`,
      }
    })

    const cursorCode = computed(() => {
      if (cursor_cursor.value) {
        return `cursor: ${cursor_cursor.value};\n`
      }
      return ''
    })
    watch(cursorCode, (newVal) => {
      ctx.emit('cursorEmit', { type: 'cursor', code: newVal })
    })
    cursor_cursor.value = props.cursorProp.cursor

    const clearObjItem = () => {
      cursor_cursor.value = ''
    }

    return {
      cursorPreview,
      cursorCode,
      cursor_cursor,
      cursor_cursors,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.preview {
  font-size: 1rem;
  text-align: center;
}
</style>
