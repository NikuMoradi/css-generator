<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div style="width: 100%; height: 100vh; display: flex">
    <div style="margin: 2rem auto; width: 98%">
      <q-tabs align="justify" outside-arrows class="activeTab bg-black text-white shadow-2">
        <q-btn-dropdown auto-close stretch flat label="Text">
          <q-list>
            <q-item clickable @click="activeTab = 'textFormatting'">
              <q-item-section>Text Formatting</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'textShadow'">
              <q-item-section>Text Shadow</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Background">
          <q-list>
            <q-item clickable @click="activeTab = 'background'">
              <q-item-section>Background</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Borders">
          <q-list>
            <q-item clickable @click="activeTab = 'border'">
              <q-item-section>Border</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'borderRadius'">
              <q-item-section>Border Radius</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'outline'">
              <q-item-section>Outline</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Box Model">
          <q-list>
            <q-item clickable @click="activeTab = 'margin'">
              <q-item-section>Margin</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'padding'">
              <q-item-section>Padding</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'size'">
              <q-item-section>Size (Width/Height)</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Layout">
          <q-list>
            <q-item clickable @click="activeTab = 'display'">
              <q-item-section>Display</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'position'">
              <q-item-section>Position</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'overflow'">
              <q-item-section>Overflow</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'columns'">
              <q-item-section>Columns</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'visibility'">
              <q-item-section>Visibility</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Transform">
          <q-list>
            <q-item clickable @click="activeTab = 'translate'">
              <q-item-section>Translate</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'rotate'">
              <q-item-section>Rotate</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'scale'">
              <q-item-section>Scale</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'skew'">
              <q-item-section>Skew</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'perspective'">
              <q-item-section>Perspective</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Effects">
          <q-list>
            <q-item clickable @click="activeTab = 'opacity'">
              <q-item-section>Opacity</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'boxShadow'">
              <q-item-section>Box Shadow</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'imageShadow'">
              <q-item-section>Image Shadow</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'imageEnhancements'">
              <q-item-section>Image Enhancements</q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Transition"> </q-btn-dropdown>
        <q-btn-dropdown auto-close stretch flat label="Miscellaneous">
          <q-list>
            <q-item clickable @click="activeTab = 'listStyle'">
              <q-item-section>List Style</q-item-section>
            </q-item>
            <q-item clickable @click="activeTab = 'cursor'">
              <q-item-section>Cursor</q-item-section>
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
        <Position @positionEmit="handleEmits" :positionProp="categorizedProperties.positionProp" />
      </div>
      <div v-show="activeTab === 'overflow'" class="container">
        <Overflow @overflowEmit="handleEmits" :overflowProp="categorizedProperties.overflowProp" />
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

      <div v-show="activeTab === 'listStyle'" class="container">
        <ListStyle
          @listStyleEmit="handleEmits"
          :listStyleProp="categorizedProperties.listStyleProp"
        />
      </div>
      <div v-show="activeTab === 'cursor'" class="container">
        <Cursor @cursorEmit="handleEmits" :cursorProp="categorizedProperties.cursorProp" />
      </div>
    </div>
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
  setup() {
    const activeTab = ref('background')

    return {
      activeTab,
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
import { ref } from 'vue'
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
