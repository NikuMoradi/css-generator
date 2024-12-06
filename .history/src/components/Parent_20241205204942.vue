<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div full-width full-height>
    <q-card style="overflow: hidden; min-width: 320px">
      <q-card-section
        :style="$q.screen.gt.md ? 'height: 83%; padding-top: 0;' : 'height: 81%; padding-top: 0;'"
        class="scroll"
      >
        <q-tabs align="justify" outside-arrows class="activeTab bg-primary text-white shadow-2">
          <q-btn-dropdown auto-close stretch flat :label="$t('style_text')">
            <q-list>
              <q-item clickable @click="activeTab = 'textFormatting'">
                <q-item-section>{{ $t('style_text_formatting') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'textShadow'">
                <q-item-section>{{ $t('style_text_shadow') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_background')">
            <q-list>
              <q-item clickable @click="activeTab = 'background'">
                <q-item-section>{{ $t('style_background') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_borders')">
            <q-list>
              <q-item clickable @click="activeTab = 'border'">
                <q-item-section>{{ $t('style_border') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'borderRadius'">
                <q-item-section>{{ $t('style_radius') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'outline'">
                <q-item-section>{{ $t('style_outline') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_box_model')">
            <q-list>
              <q-item clickable @click="activeTab = 'margin'">
                <q-item-section>{{ $t('style_margin') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'padding'">
                <q-item-section>{{ $t('style_padding') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'size'">
                <q-item-section>{{ $t('style_size') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_layout')">
            <q-list>
              <q-item clickable @click="activeTab = 'display'">
                <q-item-section>{{ $t('style_display') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'position'">
                <q-item-section>{{ $t('style_position') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'overflow'">
                <q-item-section>{{ $t('style_overflow') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'columns'">
                <q-item-section>{{ $t('style_columns') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'visibility'">
                <q-item-section>{{ $t('style_visibility') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_transform')">
            <q-list>
              <q-item clickable @click="activeTab = 'translate'">
                <q-item-section>{{ $t('style_translate') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'rotate'">
                <q-item-section>{{ $t('style_rotate') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'scale'">
                <q-item-section>{{ $t('style_scale') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'skew'">
                <q-item-section>{{ $t('style_skew') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'perspective'">
                <q-item-section>{{ $t('style_perspective') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_effects')">
            <q-list>
              <q-item clickable @click="activeTab = 'opacity'">
                <q-item-section>{{ $t('style_opacity') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'boxShadow'">
                <q-item-section>{{ $t('style_box_shadow') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'imageShadow'">
                <q-item-section>{{ $t('style_image_shadow') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'imageEnhancements'">
                <q-item-section>{{ $t('style_image_enhancements') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_transition')">
            <q-list>
              <q-item clickable @click="activeTab = 'transition'">
                <q-item-section>{{ $t('style_transition') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
          <q-btn-dropdown auto-close stretch flat :label="$t('style_miscellaneous')">
            <q-list>
              <q-item clickable @click="activeTab = 'listStyle'">
                <q-item-section>{{ $t('style_list_style') }}</q-item-section>
              </q-item>
              <q-item clickable @click="activeTab = 'cursor'">
                <q-item-section>{{ $t('style_cursor') }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
        </q-tabs>

        <!-- Render all tab components with v-show -->
        <div v-show="activeTab === 'textFormatting'" class="container">
          <TextFormatting
            @textFormattingEmit="handleEmits"
            :textFormattingProp="categorizedProperties.textFormattingProp"
          />
        </div>
        <div v-show="activeTab === 'textShadow'" class="container">
          <TextShadow
            @textShadowEmit="handleEmits"
            :textShadowProp="categorizedProperties.textShadowProp"
          />
        </div>
        <div v-show="activeTab === 'background'" class="container">
          <Background
            @backgroundEmit="handleEmits"
            :backgroundProp="categorizedProperties.backgroundProp"
          />
        </div>
        <div v-show="activeTab === 'border'" class="container">
          <Border @borderEmit="handleEmits" :borderProp="categorizedProperties.borderProp" />
        </div>
        <div v-show="activeTab === 'borderRadius'" class="container">
          <BorderRadius
            @borderRadiusEmit="handleEmits"
            :borderRadiusProp="categorizedProperties.borderRadiusProp"
          />
        </div>
        <div v-show="activeTab === 'outline'" class="container">
          <Outline @outlineEmit="handleEmits" :outlineProp="categorizedProperties.outlineProp" />
        </div>
        <div v-show="activeTab === 'boxShadow'" class="container">
          <BoxShadow
            @boxShadowEmit="handleEmits"
            :boxShadowProp="categorizedProperties.boxShadowProp"
          />
        </div>
        <div v-show="activeTab === 'margin'" class="container">
          <Margin @marginEmit="handleEmits" :marginProp="categorizedProperties.marginProp" />
        </div>
        <div v-show="activeTab === 'padding'" class="container">
          <Padding @paddingEmit="handleEmits" :paddingProp="categorizedProperties.paddingProp" />
        </div>
        <div v-show="activeTab === 'size'" class="container">
          <Size @sizeEmit="handleEmits" :sizeProp="categorizedProperties.sizeProp" />
        </div>
        <div v-show="activeTab === 'display'" class="container">
          <Display @displayEmit="handleEmits" :displayProp="categorizedProperties.displayProp" />
        </div>
        <div v-show="activeTab === 'position'" class="container">
          <Position
            @positionEmit="handleEmits"
            :positionProp="categorizedProperties.positionProp"
          />
        </div>
        <div v-show="activeTab === 'overflow'" class="container">
          <Overflow
            @overflowEmit="handleEmits"
            :overflowProp="categorizedProperties.overflowProp"
          />
        </div>
        <div v-show="activeTab === 'columns'" class="container">
          <Columns @columnsEmit="handleEmits" :columnsProp="categorizedProperties.columnsProp" />
        </div>
        <div v-show="activeTab === 'visibility'" class="container">
          <Visibility
            @visibilityEmit="handleEmits"
            :visibilityProp="categorizedProperties.visibilityProp"
          />
        </div>
        <div v-show="activeTab === 'translate'" class="container">
          <Translate
            @translateEmit="handleEmits"
            :translateProp="categorizedProperties.translateProp"
          />
        </div>
        <div v-show="activeTab === 'rotate'" class="container">
          <Rotate @rotateEmit="handleEmits" :rotateProp="categorizedProperties.rotateProp" />
        </div>
        <div v-show="activeTab === 'scale'" class="container">
          <Scale @scaleEmit="handleEmits" :scaleProp="categorizedProperties.scaleProp" />
        </div>
        <div v-show="activeTab === 'skew'" class="container">
          <Skew @skewEmit="handleEmits" :skewProp="categorizedProperties.skewProp" />
        </div>
        <div v-show="activeTab === 'perspective'" class="container">
          <Perspective
            @perspective_parent_Emit="handleEmits"
            @perspective_child_Emit="handleEmits"
            :perspectiveProp="categorizedProperties.perspectiveProp"
          />
        </div>
        <div v-show="activeTab === 'opacity'" class="container">
          <Opacity @opacityEmit="handleEmits" :opacityProp="categorizedProperties.opacityProp" />
        </div>
        <div v-show="activeTab === 'imageEnhancements'" class="container">
          <ImageEnhancements
            @imageEnhancementsEmit="handleEmits"
            :imageEnhancementsProp="categorizedProperties.imageEnhancementsProp"
          />
        </div>
        <div v-show="activeTab === 'imageShadow'" class="container">
          <ImageShadow
            @imageShadowEmit="handleEmits"
            :imageShadowProp="categorizedProperties.imageShadowProp"
          />
        </div>
        <div v-show="activeTab === 'transition'" class="container">
          <TN
            @transitionEmit="handleEmits"
            :transitionProp="categorizedProperties.transitionProp"
          />
        </div>
        <div v-show="activeTab === 'listStyle'" class="container">
          <ListStyle
            @listStyleEmit="handleEmits"
            :listStyleProp="categorizedProperties.listStyleProp"
          />
        </div>
        <div v-show="activeTab === 'cursor'" class="container">
          <Cursor @cursorEmit="handleEmits" :cursorProp="categorizedProperties.cursorProp" />
        </div>
      </q-card-section>

      <q-separator />
      <q-card-section class="btn-wrapper">
        <div>
          <q-btn
            :label="$t('save')"
            type="submit"
            color="primary"
            icon="fas fa-save"
            @click="saveBtn"
            class="save-btn"
          />
          <q-btn
            :label="$t('cancel')"
            type="reset"
            icon="fas fa-times"
            v-close-popup
            class="cancel-btn"
          />
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script>
export default {
  emits: ['updateCss'],
  props: {
    cssData: {
      type: String,
      required: false,
      default: '',
    },
    usedColors: {
      type: Array,
      required: false,
    },
  },
  setup(props, ctx) {
    const activeTab = ref('background')
    provide('usedColors', props.usedColors)
    //-----------------------------Emit to indexPage--------------------------------
    //fill the initial object with child values
    const cssObject = ref({
      background: '',
      border: '',
      borderRadius: '',
      boxShadow: '',
      columns: '',
      cursor: '',
      display: '',
      imageEnhancements: '',
      imageShadow: '',
      listStyle: '',
      margin: '',
      opacity: '',
      outline: '',
      overflow: '',
      padding: '',
      perspective_child: '',
      perspective_parent: '',
      position: '',
      rotate: '',
      scale: '',
      skew: '',
      size: '',
      textFormatting: '',
      textShadow: '',
      transition: '',
      translate: '',
      visibility: '',
    })

    const handleEmits = (data) => {
      cssObject.value[data.type] = data.code
    }

    const objectToString = () => {
      let cssString = ''
      for (const [value] of Object.entries(cssObject.value)) {
        cssString += value
      }
      return `{\n${cssString}}`
    }

    const saveBtn = () => {
      const cssString = objectToString()
      ctx.emit('updateCss', cssString)
    }

    //-----------------------------Prop to childs--------------------------------

    // Initialize an object to store categorized properties
    const categorizedProperties = reactive({
      backgroundProp: {},
      borderProp: {},
      borderRadiusProp: {},
      boxShadowProp: {},
      columnsProp: {},
      cursorProp: {},
      displayProp: {},
      imageEnhancementsProp: {},
      imageShadowProp: {},
      listStyleProp: {},
      marginProp: {},
      opacityProp: {},
      outlineProp: {},
      overflowProp: {},
      paddingProp: {},
      perspectiveProp: {},
      positionProp: {},
      rotateProp: {},
      scaleProp: {},
      skewProp: {},
      sizeProp: {},
      textFormattingProp: {},
      textShadowProp: {},
      transitionProp: {},
      translateProp: {},
      visibilityProp: {},
    })

    // Function to move property to appropriate category based on key and partial value
    function moveProperty(property) {
      const [key, ...valueParts] = property.split(':')
      const value = valueParts.join(':').trim() //for url property in bg component
      switch (key.trim()) {
        case 'background-color':
        case 'background-image':
        case 'background-position':
        case 'background-size':
        case 'background-repeat':
        case 'background-attachment':
        case 'background-origin':
        case 'background-clip':
        case 'background':
          categorizedProperties.backgroundProp[key.trim()] = value
          break
        case 'border':
        case 'border-right':
        case 'border-top':
        case 'border-bottom':
        case 'border-left':
          categorizedProperties.borderProp[key.trim()] = value
          break
        case 'border-radius':
        case 'border-top-left-radius':
        case 'border-top-right-radius':
        case 'border-bottom-right-radius':
        case 'border-bottom-left-radius':
          categorizedProperties.borderRadiusProp[key.trim()] = value
          break
        case 'box-shadow':
          categorizedProperties.boxShadowProp[key.trim()] = value
          break
        case 'opacity':
          categorizedProperties.opacityProp[key.trim()] = value
          break
        case 'outline':
        case 'outline-offset':
          categorizedProperties.outlineProp[key.trim()] = value
          break
        case 'overflow-x':
        case 'overflow-y':
          categorizedProperties.overflowProp[key.trim()] = value
          break
        case 'filter':
          if (value.includes('drop-shadow')) {
            categorizedProperties.imageShadowProp[key.trim()] = value
          } else {
            categorizedProperties.imageEnhancementsProp[key.trim()] = value
          }
          break
        case 'column-count':
          categorizedProperties.columnsProp[key.trim()] = value
          break
        case 'display':
          categorizedProperties.displayProp[key.trim()] = value
          break
        case 'visibility':
          categorizedProperties.visibilityProp[key.trim()] = value
          break
        case 'position':
        case 'top':
        case 'right':
        case 'bottom':
        case 'left':
        case 'z-index':
          categorizedProperties.positionProp[key.trim()] = value
          break
        case 'list-style':
          categorizedProperties.listStyleProp[key.trim()] = value
          break
        case 'font-family':
        case 'color':
        case 'font-size':
        case 'font-weight':
        case 'font-style':
        case 'letter-spacing':
        case 'line-height':
        case 'overflow-wrap':
        case 'direction':
        case 'text-align':
        case 'text-decoration':
        case 'text-indent':
        case 'text-transform':
        case 'white-space':
        case 'word-break':
        case 'word-spacing':
          categorizedProperties.textFormattingProp[key.trim()] = value
          break
        case 'text-shadow':
          categorizedProperties.textShadowProp[key.trim()] = value
          break
        case 'perspective':
          categorizedProperties.perspectiveProp[key.trim()] = value
        // eslint-disable-next-line no-fallthrough
        case 'transform':
          if (value.match(/rotateX\(\d+deg\)\s*rotateY\(\d+deg\)\s*rotateZ\(\d+deg\)/)) {
            categorizedProperties.rotateProp[key.trim()] = value // 3D rotation
          } else if (value.match(/rotateX\(\d+deg\)\s*rotateY\(\d+deg\)/)) {
            categorizedProperties.perspectiveProp[key.trim()] = value // Perspective
          } else if (value.match(/rotate\(\d+deg\)/)) {
            categorizedProperties.rotateProp[key.trim()] = value // 2D rotation
          } else if (value.includes('scale')) {
            categorizedProperties.scaleProp[key.trim()] = value
          } else if (value.includes('skew')) {
            categorizedProperties.skewProp[key.trim()] = value
          } else if (value.includes('translate')) {
            categorizedProperties.translateProp[key.trim()] = value
          }
          break

        case 'transition':
          categorizedProperties.transitionProp[key.trim()] = value
          break
        case 'width':
        case 'height':
        case 'min-width':
        case 'min-height':
        case 'max-width':
        case 'max-height':
          categorizedProperties.sizeProp[key.trim()] = value
          break
        case 'margin':
        case 'margin-top':
        case 'margin-left':
        case 'margin-bottom':
        case 'margin-right':
          categorizedProperties.marginProp[key.trim()] = value
          break
        case 'padding':
        case 'padding-top':
        case 'padding-right':
        case 'padding-bottom':
        case 'padding-left':
          categorizedProperties.paddingProp[key.trim()] = value
          break
        case 'cursor':
          categorizedProperties.cursorProp[key.trim()] = value
          break
        // default:
        //   // For properties not categorized, add directly
        //   categorizedProperties[key.trim()] = value;
        //   break;
      }
    }

    watch(
      () => props.cssData,
      (newVal) => {
        // Clear the previous properties
        for (let key in categorizedProperties) {
          categorizedProperties[key] = {}
        }

        // Split new properties and categorize them
        const newProperties = newVal.trim().slice(1, -1).split(';')
        newProperties.forEach((property) => {
          moveProperty(property)
        })
      },
      { immediate: true },
    )

    return {
      activeTab,
      cssObject,
      handleEmits,
      objectToString,
      saveBtn,
      categorizedProperties,
      moveProperty,
    }
  },
  components: {
    Background,
    Border,
    BorderRadius,
    BoxShadow,
    Opacity,
    Outline,
    Overflow,
    Size,
    ImageEnhancements,
    ImageShadow,
    Columns,
    Display,
    Visibility,
    ListStyle,
    TextFormatting,
    TextShadow,
    Perspective,
    Rotate,
    Scale,
    Skew,
    Translate,
    Cursor,
    Padding,
    Margin,
    Position,
  },
}
import Background from 'src/components/Background.vue'
import Border from 'src/components/Border.vue'
import BorderRadius from 'src/components/BorderRadius.vue'
import BoxShadow from 'src/components/BoxShadow.vue'
import Opacity from 'src/components/Opacity.vue'
import Outline from 'src/components/Outline.vue'
import Overflow from 'src/components/Overflow.vue'
import Size from 'src/components/Size.vue'
import ImageEnhancements from 'src/components/ImageEnhancements.vue'
import ImageShadow from 'src/components/ImageShadow.vue'
import Columns from 'src/components/Columns.vue'
import Display from 'src/components/Display.vue'
import Visibility from 'src/components/Visibility.vue'
import ListStyle from 'src/components/ListStyle.vue'
import TextFormatting from 'src/components/TextFormatting.vue'
import TextShadow from 'src/components/TextShadow.vue'
import Perspective from 'src/components/Perspective.vue'
import Rotate from 'src/components/Rotate.vue'
import Scale from 'src/components/Scale.vue'
import Skew from 'src/components/Skew.vue'
import Translate from 'src/components/Translate.vue'
import Cursor from 'src/components/Cursor.vue'
import Padding from 'src/components/Padding.vue'
import Margin from 'src/components/Margin.vue'
import Position from 'src/components/Position.vue'
import { ref, watch, reactive, provide } from 'vue'
</script>

<style scoped>
.container {
  width: 98%;
  margin: 1rem auto;
}
:deep(.no-scroll-area) {
  width: 95%;
  margin: auto auto;
}
:deep(.preview-box) {
  height: 19rem;
  border: 1px solid #00000036;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  border-radius: 6px;
  border: 1px solid #ccc;
}

:deep(.preview) {
  width: 19rem;
  height: 16rem;
  background-color: #1976d239;
  font-size: 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

:deep(.code-box) {
  height: 5.6rem;
  border: 1px solid #00000036;
  border-radius: 6px;
  padding: 0.5rem 1rem;
  font-family:
    IBM Plex Mono,
    monospace;
  white-space: pre-line;
  background: #f5f5f5;
  border: 1px solid #ccc;
  direction: initial;
}
:deep(.show-color) {
  width: 2rem;
  height: 2rem;
  border: 1px solid #00000031;
  border-radius: 50px;
}
:deep(.mb-10) {
  margin-bottom: 0.9rem;
}

:deep(.secondary-title) {
  font-size: 1.2rem;
  font-weight: 500;
  margin: 0.3rem 0 0.4rem 0;
}
:deep(.outlined-slider) {
  border: 1px solid #ccc;
  color: #666;
  font-size: 0.7rem;
  padding: 10px 11px 0px 11px;
  border-radius: 4px;
  transition: 300ms;
}
:deep(.outlined-slider):hover {
  border-color: black;
}

:deep(.slider-label) {
  display: flex;
  justify-content: space-between;
  line-height: 1;
}

.activeTab {
  position: sticky;
  top: -1.2px;
  z-index: 10;
  background-color: white;
  color: #676766;
  font-family: Segoe UI;
  width: 100%;
  height: 50px;
  border-radius: 10px;
}
.btn-wrapper {
  display: flex;
  justify-content: space-between;
}
.save-btn {
  width: 8rem;
  height: 2.5rem;
  margin-right: 10px;
}
.cancel-btn {
  width: 8rem;
  height: 2.5rem;
}

@media (max-width: 1023px) {
  :deep(.preview-box) {
    width: 95%;
    margin: 1.5rem auto;
  }
  :deep(.code-box) {
    width: 95%;
    margin: 1.5rem auto;
  }
}
</style>
