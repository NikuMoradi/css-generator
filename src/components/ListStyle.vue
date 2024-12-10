<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="List Style" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="listStyle_type"
          :options="listStyle_types"
          label="Type"
          class="mb-10"
        />
        <q-select
          outlined
          v-model="listStyle_position"
          :options="listStyle_positions"
          label="Position"
          class="mb-10"
        />
      </div>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <div class="list-style-Preview">
          <ul :style="listStylePreview">
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
            <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod!</li>
          </ul>
        </div>
      </div>
      <div class="code-box">{{ listStyleCode }}</div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['listStyleEmit'],
  props: {
    listStyleProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const listStyle_type = ref('')
    const listStyle_types = [
      '',
      'circle',
      'decimal',
      'decimal-leading-zero',
      'disc',
      'lower-alpha',
      'lower-alpha',
      'lower-roman',
      'none',
      'square',
      'upper-alpha',
      'upper-roman',
    ]
    const listStyle_position = ref('')
    const listStyle_positions = ['', 'inside', 'outside']

    const listStylePreview = computed(() => {
      if (listStyle_type.value) {
        return {
          listStyle: `${listStyle_type.value} ${listStyle_position.value}`,
        }
      }
      return 'list-style: none '
    })

    const listStyleCode = computed(() => {
      if (listStyle_type.value) {
        return `list-style: ${listStyle_type.value} ${listStyle_position.value};\n`
      } else {
        return ''
      }
    })

    watch(listStyleCode, (newVal) => {
      ctx.emit('listStyleEmit', { type: 'listStyle', code: newVal })
    })

    const parseListStyle = (style) => {
      const regex = /([\w-]+)\s*([\w-]+)?/

      const matches = style.match(regex)
      if (matches) {
        listStyle_type.value = matches[1] || ''
        listStyle_position.value = matches[2] || ''
      }
    }

    onMounted(() => {
      if (props.listStyleProp && props.listStyleProp['list-style']) {
        parseListStyle(props.listStyleProp['list-style'])
      }
    })

    const clearObjItem = () => {
      listStyle_type.value = ''
      listStyle_types.value = ''
      listStyle_position.value = ''
      listStyle_positions.value = ''
    }

    return {
      listStylePreview,
      listStyleCode,
      listStyle_type,
      listStyle_types,
      listStyle_position,
      listStyle_positions,
      clearObjItem,
    }
  },

  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.list-style-Preview {
  width: 34rem;
  height: 18.5rem;
  font-size: 1rem;
  line-height: 1.8;
}
</style>
