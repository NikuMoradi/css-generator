<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Perspective" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Length</span><span>{{ perspective_length }} px </span>
          </div>
          <q-slider
            v-model="perspective_length"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :max="500"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Rotate X</span><span>{{ perspective_rotate_x }} deg </span>
          </div>
          <q-slider
            v-model="perspective_rotate_x"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :max="360"
            class="mb-10"
          ></q-slider>
        </div>
        <div class="outlined-slider mb-10">
          <div class="slider-label">
            <span>Rotate Y</span><span>{{ perspective_rotate_y }} deg </span>
          </div>
          <q-slider
            v-model="perspective_rotate_y"
            track-size="5px"
            inner-track-color="primary"
            thumb-size="15px"
            :min="0"
            :max="360"
            class="mb-10"
          ></q-slider>
        </div>
      </div>
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="prespective-preview" :style="perspectivePreview_parent">
          <div :style="perspectivePreview_child">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi cum voluptas autem
            officiis suscipit eius distinctio, porro quibusdam dolore quae saepe ipsum iste
            necessitatibus sunt quisquam rerum, unde vel eveniet impedit ratione soluta recusandae?
            Voluptas dolor ipsam aspernatur excepturi porro!
          </div>
        </div>
      </div>
      <div class="code-box">
        <div>{{ perspectiveCode_parent }}</div>
        <div>{{ perspectiveCode_child }}</div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['perspective_parent_Emit', 'perspective_child_Emit'],
  props: {
    perspectiveProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const perspective_length = ref()
    const perspective_rotate_x = ref()
    const perspective_rotate_y = ref()
    const perspectivePreview_parent = computed(() => {
      return {
        perspective: `${perspective_length.value}px`,
      }
    })
    const perspectivePreview_child = computed(() => {
      return {
        transform: `rotateX(${perspective_rotate_x.value}deg) rotateY(${perspective_rotate_y.value}deg)`,
        transformStyle: `preserve-3d`,
      }
    })
    const perspectiveCode_parent = computed(() => {
      if (perspective_length.value !== '' && perspective_length.value !== undefined) {
        return `perspective: ${perspective_length.value}px;\n`
      } else return ''
    })
    const perspectiveCode_child = computed(() => {
      if (
        perspective_rotate_x.value !== '' &&
        perspective_rotate_y.value !== '' &&
        perspective_rotate_x.value !== undefined &&
        perspective_rotate_y.value !== undefined
      ) {
        return `transform: rotateX(${perspective_rotate_x.value}deg) rotateY(${perspective_rotate_y.value}deg);\ntransformStyle: preserve-3d;\n`
      } else return ''
    })
    watch(perspectiveCode_parent, (newVal) => {
      ctx.emit('perspective_parent_Emit', {
        type: 'perspective_parent',
        code: newVal,
      })
    })
    watch(perspectiveCode_child, (newVal) => {
      ctx.emit('perspective_child_Emit', {
        type: 'perspective_child',
        code: newVal,
      })
    })
    Object.entries(props.perspectiveProp).forEach(([key, value]) => {
      switch (key) {
        case 'perspective': {
          const perspectiveMatch = value.match(/(\d+)px/)
          if (perspectiveMatch) {
            perspective_length.value = Number(perspectiveMatch[1])
          }
          break
        }
        case 'transform': {
          const transformMatch = value.match(/rotateX\((\d+)deg\)?\s*rotateY\((\d+)deg\)?/)

          if (transformMatch) {
            perspective_rotate_x.value = Number(transformMatch[1])
            perspective_rotate_y.value = Number(transformMatch[2])
          }
          break
        }
      }
    })

    const clearObjItem = () => {
      perspective_length.value = ''
      perspective_rotate_x.value = ''
      perspective_rotate_y.value = ''
      perspectivePreview_parent.value.perspective = ''
      perspectivePreview_child.value.transform = ''
    }

    return {
      perspectivePreview_parent,
      perspectivePreview_child,
      perspectiveCode_parent,
      perspectiveCode_child,
      perspective_length,
      perspective_rotate_x,
      perspective_rotate_y,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.prespective-preview {
  width: 19rem;
  height: 16rem;
  padding: 1rem;
  background-color: #1976d239;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1rem;
}
</style>
