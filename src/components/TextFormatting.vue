<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Text Formatting" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="textFormatting_language"
            :options="textFormatting_languages"
            label="Sample Text Language"
            class="mb-10"
          />

          <div class="row q-col-gutter-sm">
            <div class="col-6">
              <q-select
                outlined
                v-model="textFormatting_fontFamily"
                :options="textFormatting_fontFamily_eng"
                label="Font Family"
                class="mb-10"
                v-if="textFormatting_language == 'English' || textFormatting_language == 'German'"
              />
              <q-select
                outlined
                v-model="textFormatting_fontFamily"
                :options="textFormatting_fontFamily_pre"
                label="Font Family"
                class="mb-10"
                v-if="textFormatting_language == 'Persian' || textFormatting_language == 'Arabic'"
              />
            </div>
            <div class="col-6">
              <q-input label="Text Color" outlined v-model="textFormatting_textColor">
                <template v-slot:append>
                  <div
                    class="show-color"
                    :style="{
                      backgroundColor: textFormatting_textColor,
                    }"
                  ></div>
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-color
                      v-model="textFormatting_textColor"
                      no-header-tabs
                      :palette="colorPalette"
                    />
                  </q-popup-proxy>
                </template>
              </q-input>
            </div>
          </div>
          <div class="row q-col-gutter-x-sm">
            <div class="col-6">
              <q-input
                v-model.number="textFormatting_fontSize"
                label="Font Size"
                type="number"
                outlined
                min="4"
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="textFormatting_fontSize_unitType"
                :options="textFormatting_fontSize_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <div class="row q-col-gutter-x-sm">
            <div class="col-xs-6 col-sm-9 col-lg-10">
              <q-select
                outlined
                v-model="textFormatting_fontWeight"
                :options="textFormatting_fontWeights"
                label="Text Weight"
                class="mb-10"
              />
            </div>
            <div class="col-xs-6 col-sm-3 col-lg-2">
              <div class="outlined-checkbox">
                <div class="checkbox-label">
                  <span>Font style</span>
                </div>
                <q-checkbox
                  v-model="textFormatting_italic"
                  label="Italic"
                  size="sm"
                  class="mb-10"
                />
              </div>
            </div>
          </div>

          <q-input
            v-model.number="textFormatting_lineHeight"
            label="Line Height"
            type="number"
            outlined
            min="0"
            step="0.2"
            class="mb-10"
          />

          <q-select
            outlined
            v-model="textFormatting_textAlign"
            :options="textFormatting_textAligns"
            label="Text Align"
            class="mb-10"
          />
          <q-select
            outlined
            v-model="textFormatting_direction"
            :options="textFormatting_directions"
            label="Text Direction"
            class="mb-10"
          />
          <div class="row q-col-gutter-x-sm">
            <div class="col-6">
              <q-input
                v-model.number="textFormatting_letterSpacing"
                label="Letter Spacing"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="textFormatting_letterSpacing_unitType"
                :options="textFormatting_letterSpacing_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <div class="row q-col-gutter-x-sm">
            <div class="col-6">
              <q-input
                v-model.number="textFormatting_wordSpacing"
                label="Word Spacing"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="textFormatting_wordSpacing_unitType"
                :options="textFormatting_wordSpacing_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>

          <div class="row q-col-gutter-x-sm">
            <div class="col-6">
              <q-input
                v-model.number="textFormatting_textIndent"
                label="Text Indent"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="textFormatting_textIndent_unitType"
                :options="textFormatting_textIndent_unitTypes"
                label="Unit"
                class="mb-10"
              />
            </div>
          </div>
          <q-select
            outlined
            v-model="textFormatting_textTransform"
            :options="textFormatting_textTransforms"
            label="Text Transform"
            class="mb-10"
          />
          <q-select
            outlined
            v-model="textFormatting_overflowWrap"
            :options="textFormatting_overflowWraps"
            label="Overflow Wrap"
            class="mb-10"
          />

          <q-select
            outlined
            v-model="textFormatting_whiteSpace"
            :options="textFormatting_whiteSpaces"
            label="White Space"
            class="mb-10"
          />
          <q-select
            outlined
            v-model="textFormatting_wordBreak"
            :options="textFormatting_wordBreaks"
            label="Word Breaks"
            class="mb-10"
          />
          <div class="row q-col-gutter-sm">
            <div class="col-xs-6 col-sm-4">
              <q-select
                outlined
                v-model="textFormatting_textDecoration_type"
                :options="textFormatting_textDecoration_types"
                label="Text Decoration Type"
                class="mb-10"
              />
            </div>
            <div class="col-xs-6 col-sm-4">
              <q-select
                outlined
                v-model="textFormatting_textDecoration_style"
                :options="textFormatting_textDecoration_styles"
                label="Text Decoration Style"
                class="mb-10"
              />
            </div>
            <div class="col-xs-6 col-sm-4">
              <q-input
                label="Text Decoration Color"
                outlined
                v-model="textFormatting_textDecoration_color"
                class="large"
              >
                <template v-slot:append>
                  <div
                    class="show-color"
                    :style="{
                      backgroundColor: textFormatting_textDecoration_color,
                    }"
                  ></div>
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-color
                      v-model="textFormatting_textDecoration_color"
                      no-header-tabs
                      :palette="colorPalette"
                    />
                  </q-popup-proxy>
                </template>
              </q-input>
            </div>
          </div>
        </div>
      </q-scroll-area>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box">
        <blockquote class="text-formatting-preview" :style="textFormattingPreview">
          <p v-if="textFormatting_language == 'English' || textFormatting_language == 'German'">
            Lorem ipsum dolor sit amet consectetur adipisicing elit.Repellendus exercitationem culpa
            laudantium, sapiente porro quod est eveniet ratione dolore earum voluptas ut
            necessitatibus nemo eligendi, quas obcaecati! Provident natus sint eius ipsa adipisci
            voluptatibus, nesciunt eum incidunt libero ratione nam placeat quasi ipsam quibusdam,
            iure culpa molestias autem quas esse?
          </p>
          <p v-if="textFormatting_language == 'Persian' || textFormatting_language == 'Arabic'">
            هر روز فرصتی است برای یادگیری و خلق ایده‌های نو. دنیای تکنولوژی همواره در حال تغییر است
            و شما می‌توانید با پذیرش دانش جدید، در مسیر پیشرفت گام بردارید. به یاد داشته باشید که هر
            خط کد، فرصتی برای نوآوری و خلاقیت است. سایت‌های حرفه‌ای و کاربرپسند، نتیجه‌ی تلاش و هنر
            شماست. پس با اشتیاق و انگیزه به یادگیری ادامه دهید و جهانی از امکانات را پیش روی کاربران
            خود بگشایید. هر آن‌چه که ذهن انسان بتواند تصور و باور کند، دست‌یافتنی است
          </p>
        </blockquote>
      </div>

      <div class="code-box">
        <q-scroll-area style="height: 7rem">
          {{ textFormattingCode }}
        </q-scroll-area>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['textFormattingEmit'],
  props: {
    textFormattingProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const colorPalette = inject('usedColors')
    const textFormatting_language = ref('English')
    const textFormatting_languages = ['Persian', 'English', 'Arabic', 'German']
    const textFormatting_italic = ref(false)
    const textFormatting_fontFamily = ref('')
    const textFormatting_fontFamily_eng = [
      '',
      'Arial',
      'Verdana',
      'Helvetica',
      'Tahoma',
      'Trebuchet MS',
      'Times New Roman',
      'Georgia',
      'Garamond',
      'Courier New',
      'Brush Script MT',
      'Lucida Sans',
      'Palatino',
      'Bookman',
      'New Century Schoolbook',
      'American Typewriter',
      'Andale Mono',
      'Comic Sans MS',
      'Impact',
      'Serif',
      'Sans-Serif',
      'Monospace',
      'Cursive',
      'Fantasy',
      'MS Sans Serif',
      'MS Serif',
      'Lucida Console',
      'Lucida Sans Unicode',
      'Lucida Grande',
      'Lucida Bright',
      'Geneva',
      'Charcoal',
      'Optima',
      'Baskerville',
      'Perpetua',
      'Rockwell',
      'Consolas',
      'Monaco',
      'Didot',
      'Franklin Gothic Medium',
      'ITC Franklin Gothic',
      'Futura',
      'Gill Sans',
      'Cambria',
      'Calisto MT',
      'Candara',
      'Century Gothic',
      'Franklin Gothic',
      'High Tower Text',
      'Hoefler Text',
      'Joanna',
      'Malgun Gothic',
      'Segoe UI',
      'Myriad Pro',
      'Minion Pro',
      'Adobe Garamond Pro',
      'Adobe Caslon Pro',
      'Bembo',
      'Goudy Old Style',
      'Big Caslon',
      'Bodoni MT',
      'Clarendon',
      'Footlight MT Light',
      'Bell MT',
      'Bauhaus 93',
      'Bernard MT Condensed',
      'Broadway',
      'Brush Script Std',
      'Californian FB',
      'Centaur',
      'Chiller',
      'Colonna MT',
      'Cooper Black',
      'Copperplate Gothic Bold',
      'Copperplate Gothic Light',
      'Elephant',
      'Engravers MT',
      'Eras Bold ITC',
      'Eras Medium ITC',
      'Felix Titling',
      'Fortune City',
      'Freestyle Script',
      'French Script MT',
      'Gigi',
      'Gill Sans Ultra Bold',
      'Gloucester MT Extra Condensed',
      'Goudy Stout',
      'Harlow Solid Italic',
      'Harrington',
      'Haettenschweiler',
      'Imprint MT Shadow',
      'Informal Roman',
      'Blackadder ITC',
      'Edwardian Script ITC',
      'Kristen ITC',
      'Jokerman',
      'Juice ITC',
      'Kunstler Script',
      'Wide Latin',
      'Lucida Calligraphy',
      'Lucida Handwriting',
      'Magneto',
      'Matura MT Script Capitals',
      'Mistral',
      'Modern No. 20',
      'Monotype Corsiva',
      'Niagara Solid',
      'Niagara Engraved',
      'Old English Text MT',
      'Onyx',
      'Papyrus',
      'Parchment',
      'Playbill',
      'Poor Richard',
      'Pristina',
      'Rage Italic',
      'Ravie',
      'Script MT Bold',
      'Showcard Gothic',
      'Snap ITC',
      'Stencil',
      'Tempus Sans ITC',
      'Viner Hand ITC',
      'Vivaldi',
      'Vladimir Script',
      'Wide Latin',
      'Unset',
    ]
    const textFormatting_fontFamily_pre = [
      '',
      'Nazanin',
      'Yekan',
      'Vazir',
      'Shabnam',
      'Samim',
      'Nahid',
      'Ekan',
      'Parastoo',
      'Tanha',
      'Sahel',
    ]

    const textFormatting_textColor = ref('')

    const textFormatting_fontSize = ref('')

    const textFormatting_fontWeight = ref('')
    const textFormatting_fontWeights = [
      '',
      '100',
      '200',
      '300',
      '400',
      '500',
      '600',
      '700',
      '800',
      '900',
    ]

    const textFormatting_letterSpacing = ref('')

    const textFormatting_lineHeight = ref('')

    const textFormatting_overflowWrap = ref('')
    const textFormatting_overflowWraps = ['', 'anywhere', 'break-word', 'normal']

    const textFormatting_direction = ref('')
    const textFormatting_directions = ['', 'ltr', 'rtl']

    const textFormatting_textAlign = ref('')
    const textFormatting_textAligns = ['', 'center', 'justify', 'left', 'right']

    const textFormatting_textDecoration_type = ref('')
    const textFormatting_textDecoration_types = ['', 'line-through', 'overline', 'underline']
    const textFormatting_textDecoration_style = ref('')
    const textFormatting_textDecoration_styles = ['', 'dashed', 'dotted', 'double', 'solid', 'wavy']

    const textFormatting_textDecoration_color = ref('')

    const textFormatting_textIndent = ref('')

    const textFormatting_textTransform = ref('')
    const textFormatting_textTransforms = ['', 'capitalize', 'lowercase', 'uppercase']

    const textFormatting_whiteSpace = ref('')
    const textFormatting_whiteSpaces = ['', 'nowrap', 'pre', 'pre-line', 'pre-wrap']

    const textFormatting_wordBreak = ref('')
    const textFormatting_wordBreaks = ['', 'break-all', 'break-word', 'keep-all', 'normal']

    const textFormatting_wordSpacing = ref('')

    const textFormatting_fontSize_unitType = ref('')
    const textFormatting_fontSize_unitTypes = [
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

    const textFormatting_letterSpacing_unitType = ref('')
    const textFormatting_letterSpacing_unitTypes = [
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

    const textFormatting_wordSpacing_unitType = ref('')
    const textFormatting_wordSpacing_unitTypes = [
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
    const textFormatting_textIndent_unitType = ref('')
    const textFormatting_textIndent_unitTypes = [
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
    watch(textFormatting_textColor, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        textFormatting_textColor.value = ''
      }
    })
    watch(textFormatting_textDecoration_color, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        textFormatting_textDecoration_color.value = ''
      }
    })

    const textFormattingPreview = computed(() => {
      const hasTextDecorationValues =
        textFormatting_textDecoration_type.value &&
        textFormatting_textDecoration_style.value &&
        textFormatting_textDecoration_color.value

      return {
        fontFamily: `${textFormatting_fontFamily.value}`,
        color: `${textFormatting_textColor.value}`,
        fontSize: `${textFormatting_fontSize.value}${textFormatting_fontSize_unitType.value}`,
        fontWeight: `${textFormatting_fontWeight.value}`,
        letterSpacing: `${textFormatting_letterSpacing.value}${textFormatting_letterSpacing_unitType.value}`,
        lineHeight: `${textFormatting_lineHeight.value}`,
        overflowWrap: `${textFormatting_overflowWrap.value}`,
        direction: `${textFormatting_direction.value}`,
        textAlign: `${textFormatting_textAlign.value}`,
        ...(hasTextDecorationValues && {
          textDecoration: `${textFormatting_textDecoration_type.value} ${textFormatting_textDecoration_style.value} ${textFormatting_textDecoration_color.value}`,
        }),
        textIndent: `${textFormatting_textIndent.value}${textFormatting_textIndent_unitType.value}`,
        textTransform: `${textFormatting_textTransform.value}`,
        whiteSpace: `${textFormatting_whiteSpace.value}`,
        wordBreak: `${textFormatting_wordBreak.value}`,
        wordSpacing: `${textFormatting_wordSpacing.value}${textFormatting_wordSpacing_unitType.value}`,
        fontStyle: textFormatting_italic.value ? 'italic' : 'normal',
      }
    })

    const textFormattingCode = computed(() => {
      let code = ''

      // Most frequently used properties
      if (textFormatting_fontFamily.value) {
        code += `font-family: ${textFormatting_fontFamily.value};\n`
      }
      if (textFormatting_textColor.value) {
        code += `color: ${textFormatting_textColor.value};\n`
      }
      if (textFormatting_fontSize.value && textFormatting_fontSize_unitType.value) {
        code += `font-size: ${textFormatting_fontSize.value}${textFormatting_fontSize_unitType.value};\n`
      }
      if (textFormatting_fontWeight.value) {
        code += `font-weight: ${textFormatting_fontWeight.value};\n`
      }
      if (textFormatting_italic.value) {
        code += `font-style: italic;\n`
      }
      if (textFormatting_lineHeight.value) {
        code += `line-height: ${textFormatting_lineHeight.value};\n`
      }
      if (textFormatting_textAlign.value) {
        code += `text-align: ${textFormatting_textAlign.value};\n`
      }
      if (textFormatting_direction.value) {
        code += `direction: ${textFormatting_direction.value};\n`
      }
      if (textFormatting_letterSpacing.value && textFormatting_letterSpacing_unitType.value) {
        code += `letter-spacing: ${textFormatting_letterSpacing.value}${textFormatting_letterSpacing_unitType.value};\n`
      }
      if (textFormatting_wordSpacing.value && textFormatting_wordSpacing_unitType.value) {
        code += `word-spacing: ${textFormatting_wordSpacing.value}${textFormatting_wordSpacing_unitType.value};\n`
      }
      if (textFormatting_textIndent.value && textFormatting_textIndent_unitType.value) {
        code += `text-indent: ${textFormatting_textIndent.value}${textFormatting_textIndent_unitType.value};\n`
      }
      if (textFormatting_textTransform.value) {
        code += `text-transform: ${textFormatting_textTransform.value};\n`
      }
      if (textFormatting_overflowWrap.value) {
        code += `overflow-wrap: ${textFormatting_overflowWrap.value};\n`
      }
      if (textFormatting_whiteSpace.value) {
        code += `white-space: ${textFormatting_whiteSpace.value};\n`
      }
      if (textFormatting_wordBreak.value) {
        code += `word-break: ${textFormatting_wordBreak.value};\n`
      }

      // Less frequently used properties
      if (
        textFormatting_textDecoration_type.value ||
        textFormatting_textDecoration_style.value ||
        textFormatting_textDecoration_color.value
      ) {
        code += `text-decoration: ${textFormatting_textDecoration_type.value} ${textFormatting_textDecoration_style.value} ${textFormatting_textDecoration_color.value};\n`
      }

      return code
    })
    watch(textFormattingCode, (newVal) => {
      ctx.emit('textFormattingEmit', { type: 'textFormatting', code: newVal })
    })
    Object.entries(props.textFormattingProp).forEach(([key, value]) => {
      switch (key) {
        case 'font-family':
          textFormatting_fontFamily.value = value
          break
        case 'color':
          textFormatting_textColor.value = value
          break
        case 'font-size': {
          const fontSizeMatch = value.match(/(\d+)(\D+)/)
          if (fontSizeMatch) {
            textFormatting_fontSize.value = fontSizeMatch[1]
            textFormatting_fontSize_unitType.value = fontSizeMatch[2]
          }
          break
        }
        case 'font-weight':
          textFormatting_fontWeight.value = value
          break
        case 'font-style':
          textFormatting_italic.value = value === 'italic'
          break
        case 'letter-spacing': {
          const letterSpacingMatch = value.match(/(\d+)(\D+)/)
          if (letterSpacingMatch) {
            textFormatting_letterSpacing.value = letterSpacingMatch[1]
            textFormatting_letterSpacing_unitType.value = letterSpacingMatch[2]
          }
          break
        }
        case 'line-height':
          textFormatting_lineHeight.value = value
          break
        case 'overflow-wrap':
          textFormatting_overflowWrap.value = value
          break
        case 'direction':
          textFormatting_direction.value = value
          break
        case 'text-align':
          textFormatting_textAlign.value = value
          break
        case 'text-decoration': {
          const textDecorationParts = value.split(' ')
          textFormatting_textDecoration_type.value = textDecorationParts[0]
          if (textDecorationParts[1]) {
            textFormatting_textDecoration_style.value = textDecorationParts[1]
          }
          if (textDecorationParts[2]) {
            textFormatting_textDecoration_color.value = textDecorationParts[2]
          }
          break
        }
        case 'text-indent': {
          const textIndentMatch = value.match(/(\d+)(\D+)/)
          if (textIndentMatch) {
            textFormatting_textIndent.value = textIndentMatch[1]
            textFormatting_textIndent_unitType.value = textIndentMatch[2]
          }
          break
        }
        case 'text-transform':
          textFormatting_textTransform.value = value
          break
        case 'white-space':
          textFormatting_whiteSpace.value = value
          break
        case 'word-break':
          textFormatting_wordBreak.value = value
          break
        case 'word-spacing': {
          const wordSpacingMatch = value.match(/(\d+)(\D+)/)
          if (wordSpacingMatch) {
            textFormatting_wordSpacing.value = wordSpacingMatch[1]
            textFormatting_wordSpacing_unitType.value = wordSpacingMatch[2]
          }
          break
        }
        default:
          break
      }
    })

    const clearObjItem = () => {
      textFormatting_fontFamily.value = ''
      textFormatting_fontFamily_eng.value = ''
      textFormatting_fontFamily_pre.value = ''
      textFormatting_textColor.value = ''
      textFormatting_fontSize.value = ''
      textFormatting_fontWeight.value = ''
      textFormatting_italic.value = ''
      textFormatting_letterSpacing.value = ''
      textFormatting_lineHeight.value = ''
      textFormatting_overflowWrap.value = ''
      textFormatting_textAlign.value = ''
      textFormatting_textIndent.value = ''
      textFormatting_direction.value = ''
      textFormatting_textDecoration_type.value = ''
      textFormatting_textDecoration_style.value = ''
      textFormatting_textDecoration_color.value = ''
      textFormatting_textTransform.value = ''
      textFormatting_whiteSpace.value = ''
      textFormatting_wordBreak.value = ''
      textFormatting_wordSpacing.value = ''
      textFormatting_fontSize_unitType.value = ''
      textFormatting_letterSpacing_unitType.value = ''
      textFormatting_wordSpacing_unitType.value = ''
      textFormatting_textIndent_unitType.value = ''
      textFormattingPreview.value.textDecoration = ''
    }
    return {
      colorPalette,
      textFormattingPreview,
      textFormattingCode,
      textFormatting_language,
      textFormatting_languages,
      textFormatting_italic,
      textFormatting_fontFamily,
      textFormatting_fontFamily_eng,
      textFormatting_fontFamily_pre,
      textFormatting_textColor,
      textFormatting_fontSize,
      textFormatting_fontWeight,
      textFormatting_fontWeights,
      textFormatting_letterSpacing,
      textFormatting_lineHeight,
      textFormatting_overflowWrap,
      textFormatting_overflowWraps,
      textFormatting_textAlign,
      textFormatting_textAligns,
      textFormatting_textIndent,
      textFormatting_direction,
      textFormatting_directions,
      textFormatting_textDecoration_type,
      textFormatting_textDecoration_types,
      textFormatting_textDecoration_style,
      textFormatting_textDecoration_styles,
      textFormatting_textDecoration_color,
      textFormatting_textTransform,
      textFormatting_textTransforms,
      textFormatting_whiteSpace,
      textFormatting_whiteSpaces,
      textFormatting_wordBreak,
      textFormatting_wordBreaks,
      textFormatting_wordSpacing,
      textFormatting_fontSize_unitType,
      textFormatting_fontSize_unitTypes,
      textFormatting_letterSpacing_unitType,
      textFormatting_letterSpacing_unitTypes,
      textFormatting_wordSpacing_unitType,
      textFormatting_wordSpacing_unitTypes,
      textFormatting_textIndent_unitType,
      textFormatting_textIndent_unitTypes,
      clearObjItem,
    }
  },

  components: {
    SubHeader,
  },
}
</script>

<style scoped>
.text-formatting-preview {
  width: 32rem;
  height: 17rem;
  line-height: 1.9;
}
.align-center {
  display: flex;
  align-items: baseline;
}
.outlined-checkbox {
  height: 3.48rem;
  padding: 0.6rem 0rem 0 0.8rem;
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
  display: flex;
  justify-content: space-between;
  line-height: 0.8;
}
</style>
