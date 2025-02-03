<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Background" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-md-6 col-sm-12 col-xs-12">
      <q-scroll-area style="height: 65vh">
        <div style="padding: 0 1rem">
          <q-select
            outlined
            v-model="bg_selection"
            :options="bg_selection_options"
            label="Background Type"
            class="mb-10"
          />

          <div v-if="bg_selection === 'Single Color / Image'">
            <q-input label="Color" outlined v-model="bg_backgroundColor" class="mb-10">
              <template v-slot:append>
                <div class="show-color" :style="{ backgroundColor: bg_backgroundColor }"></div>
                <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                  <q-color v-model="bg_backgroundColor" no-header-tabs :palette="colorPalette" />
                </q-popup-proxy>
              </template>
            </q-input>
          </div>

          <div
            v-if="bg_selection === 'Gradient Color'"
            class="gradient-wrapper row q-my-lg q-col-gutter-sm"
          >
            <div class="col-xs-12 col-sm-9">
              <q-select
                outlined
                v-model="bg_gradient_type"
                :options="bg_gradient_types"
                label="Type"
              />
            </div>
            <div class="col-xs-12 col-sm-3">
              <q-input
                v-model.number="bg_gradient_angle"
                label="Angle (deg)"
                type="number"
                outlined
                min="0"
                v-if="bg_gradient_type == 'linear-gradient'"
              />
            </div>
            <div class="col-xs-6 col-sm-3 col-md-3">
              <q-input label="Color" outlined v-model="bg_gradient_color_1">
                <template v-slot:append>
                  <div class="show-color" :style="{ backgroundColor: bg_gradient_color_1 }"></div>
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-color v-model="bg_gradient_color_1" no-header-tabs :palette="colorPalette" />
                  </q-popup-proxy>
                </template>
              </q-input>
            </div>
            <div class="col-xs-6 col-sm-3 col-md-3">
              <q-input
                v-model.number="bg_gradient_position_1"
                label="Position (%)"
                type="number"
                outlined
                min="0"
              />
            </div>
            <div class="col-xs-6 col-sm-3 col-md-3">
              <q-input label="Color" outlined v-model="bg_gradient_color_2">
                <template v-slot:append>
                  <div class="show-color" :style="{ backgroundColor: bg_gradient_color_2 }"></div>
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-color v-model="bg_gradient_color_2" no-header-tabs :palette="colorPalette" />
                  </q-popup-proxy>
                </template>
              </q-input>
            </div>
            <div class="col-xs-6 col-sm-3 col-md-3">
              <q-input
                v-model.number="bg_gradient_position_2"
                label="Position (%)"
                type="number"
                outlined
                min="0"
                class="mb-10"
              />
            </div>
            <div class="col-12">
              <q-select
                outlined
                v-model="bg_gradient_option"
                :options="bg_gradient_options"
                option-label="name"
                option-value="value"
                label="Predefined CSS Gradients"
                class="q-mb-md"
              />
            </div>
          </div>

          <div
            class="image-wrapper row q-my-lg q-col-gutter-sm"
            v-if="bg_selection === 'Single Color / Image'"
          >
            <div class="col-12">
              <q-file
                outlined
                v-model="bg_imageFile"
                label="Image File"
                max-files="1"
                accept=".jpg, .jpeg, .png"
                @update:model-value="handleUpload"
              >
                <template v-slot:append>
                  <div
                    @click.stop.prevent="((bg_imageFile = null), (fileUrl = null))"
                    v-if="!isEmpty(bg_imageFile)"
                  >
                    <i class="fa fa-times"></i>
                  </div>
                  <div v-if="isEmpty(bg_imageFile)">
                    <i class="fa fa-upload"></i>
                  </div>
                </template>
              </q-file>
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="bg_image_position"
                :options="bg_image_positions"
                label="Position"
              />
            </div>
            <div class="col-6">
              <q-select outlined v-model="bg_image_size" :options="bg_image_sizes" label="Size" />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="bg_image_repeat"
                :options="bg_image_repeats"
                label="Repeat"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="bg_image_attachment"
                :options="bg_image_attachments"
                label="Attachment"
              />
            </div>
            <div class="col-6">
              <q-select
                outlined
                v-model="bg_image_origin"
                :options="bg_image_origins"
                label="Origin"
              />
            </div>
            <div class="col-6">
              <q-select outlined v-model="bg_image_clip" :options="bg_image_clips" label="Clip" />
            </div>
          </div>
        </div>
      </q-scroll-area>
    </div>
    <div class="col-xs-12 col-md-5 q-gutter-y-lg">
      <div class="preview-box" :style="backgroundPreview"></div>

      <div class="code-box">
        <q-scroll-area style="height: 7rem">
          {{ backgroundCode }}
        </q-scroll-area>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch, onMounted, inject } from 'vue'
import SubHeader from './SubHeader.vue'

export default {
  emits: ['backgroundEmit'],
  props: {
    backgroundProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const usedColors = inject('usedColors')
    const colorPalette = computed(() => usedColors)
    const bg_selection = ref('Single Color / Image')
    const bg_selection_options = ['Single Color / Image', 'Gradient Color']

    const bg_backgroundColor = ref('')
    // Image
    const bg_imageFile = ref(null)
    const fileUrl = ref('')
    const handleUpload = () => {
      if (bg_imageFile.value) {
        fileUrl.value = URL.createObjectURL(bg_imageFile.value)
      }
    }

    const bg_image_position = ref('')
    const bg_image_positions = [
      '',
      'center bottom',
      'center center',
      'center top',
      'left bottom',
      'left center',
      'left top',
      'right bottom',
      'right center',
      'right top',
    ]

    const bg_image_size = ref('')
    const bg_image_sizes = ['', 'auto', 'contain', 'cover']

    const bg_image_repeat = ref('')
    const bg_image_repeats = ['', 'repeat', 'no-repeat']

    const bg_image_attachment = ref('')
    const bg_image_attachments = ['', 'fixed', 'local', 'scroll']

    const bg_image_origin = ref('')
    const bg_image_origins = ['', 'border-box', 'padding-box', 'content-box']

    const bg_image_clip = ref('')
    const bg_image_clips = ['', 'border-box', 'padding-box', 'content-box', 'text']

    const isEmpty = (input) => {
      return !input
    }
    // Gradient
    const bg_gradient_color_1 = ref('')
    const bg_gradient_color_2 = ref('')
    const bg_gradient_position_1 = ref('')
    const bg_gradient_position_2 = ref('')
    const bg_gradient_angle = ref('')
    const bg_gradient_type = ref('')
    const bg_gradient_types = ['', 'linear-gradient', 'radial-gradient']
    const bg_gradient_option = ref()
    const bg_gradient_options = ref([
      '',
      'linear-gradient(90deg, #fbc2eb 0%, #a6c0fe 100%)', // Pink to Blue
      'linear-gradient(36deg, #2f3661 18%, #57b2c9 77%)', // Mint Green to Blue
      'linear-gradient(36deg, #6fd695 18%, #57b2c9 77%)', // Mint Green to Blue
      'linear-gradient(180deg, #ffafbd 0%, #ffc3a0 100%)', // Soft Pink
      'linear-gradient(135deg, #e2e2e2 0%, #c9d6ff 100%)', // Cloudy
      'linear-gradient(45deg, #ff9a9e 0%, #fad0c4 100%)', // Peach to Pink
      'linear-gradient(90deg, #f3ec78 0%, #af4261 100%)', // Warm Sunset
      'linear-gradient(60deg, #ff6b6b 0%, #f06595 100%)', // Pink to Purple
      'linear-gradient(90deg, #a1c4fd 0%, #c2e9fb 100%)', // Cool Blue
      'linear-gradient(120deg, #f6d365 0%, #fda085 100%)', // Warm Gradient
      'linear-gradient(90deg, #f093fb 0%, #f5576c 100%)', // Purple to Pink
      'linear-gradient(180deg, #fc00ff 0%, #00dbde 100%)', // Neon Pink to Blue
      'linear-gradient(180deg, #ff5f6d 0%, #ffc371 100%)', // Coral to Gold
      'linear-gradient(60deg, #abecd6 0%, #fbed96 100%)', // Mint to Yellow
      'linear-gradient(120deg, #a18cd1 0%, #fbc2eb 100%)', // Purple to Pink
      'linear-gradient(180deg, #fdfbfb 0%, #ebedee 100%)', // Light Gray
      'linear-gradient(180deg, #ffecd2 0%, #fcb69f 100%)', // Cream to Pink
      'linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%)', // Blue to White
    ])

    // Color input Validations
    watch(bg_backgroundColor, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        bg_backgroundColor.value = ''
      }
    })
    watch(bg_gradient_color_1, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        bg_gradient_color_1.value = ''
      }
    })
    watch(bg_gradient_color_2, (newVal) => {
      if (!/^#[0-9A-F]{6}$/i.test(newVal)) {
        bg_gradient_color_2.value = ''
      }
    })
    // Assign Predefined Linear gradient to respective refs
    watch(bg_gradient_option, (newVal) => {
      if (newVal) {
        // Regular expression to match gradient type and values
        const gradientDetails = newVal.match(/(linear-gradient|radial-gradient)\(([^)]+)\)/)

        if (gradientDetails) {
          const type = gradientDetails[1]
          const values = gradientDetails[2].split(/,(?![^()]*\))/) // Split by comma outside parentheses

          // Update gradient type
          bg_gradient_type.value = type

          if (type === 'linear-gradient') {
            // Extract angle and color stops
            const angleMatch = values[0].match(/(\d+)deg/)
            const angle = angleMatch ? angleMatch[1] : '0'
            bg_gradient_angle.value = angle

            // Set color stops
            const colorStops = values.slice(1) // Skip angle
            if (colorStops.length > 0) {
              const [color1, position1] = colorStops[0].trim().split(' ')
              bg_gradient_color_1.value = color1 || '#000000'
              bg_gradient_position_1.value = position1 ? position1.replace('%', '') : '0'
            }
            if (colorStops.length > 1) {
              const [color2, position2] = colorStops[1].trim().split(' ')
              bg_gradient_color_2.value = color2 || '#ffffff'
              bg_gradient_position_2.value = position2 ? position2.replace('%', '') : '100%'
            }
          } else if (type === 'radial-gradient') {
            // Set color stops
            const colorStops = values
            if (colorStops.length > 0) {
              const [color1, position1] = colorStops[0].trim().split(' ')
              bg_gradient_color_1.value = color1 || '#000000'
              bg_gradient_position_1.value = position1 ? position1.replace('%', '') : '0'
            }
            if (colorStops.length > 1) {
              const [color2, position2] = colorStops[1].trim().split(' ')
              bg_gradient_color_2.value = color2 || '#ffffff'
              bg_gradient_position_2.value = position2 ? position2.replace('%', '') : '100%'
            }
          }
        } else {
          // Handle cases where the gradient string does not match expected format
          bg_gradient_type.value = ''
          bg_gradient_color_1.value = ''
          bg_gradient_color_2.value = ''
          bg_gradient_position_1.value = ''
          bg_gradient_position_2.value = ''
          bg_gradient_angle.value = ''
        }
      }
    })

    //Check inputs to have non-empty values
    const isSingleColor = computed(() => {
      return (
        bg_backgroundColor.value ||
        bg_image_attachment.value ||
        bg_image_clip.value ||
        bg_image_origin.value ||
        bg_image_position.value ||
        bg_image_repeat.value ||
        bg_image_size.value ||
        bg_imageFile.value
      )
    })
    const isLinear = computed(() => {
      return (
        bg_gradient_color_1.value &&
        bg_gradient_color_2.value &&
        bg_gradient_position_1.value &&
        bg_gradient_position_2.value &&
        bg_gradient_angle.value &&
        bg_gradient_type.value
      )
    })
    const isRadial = computed(() => {
      return (
        bg_gradient_color_1.value &&
        bg_gradient_color_2.value &&
        bg_gradient_position_1.value &&
        bg_gradient_position_2.value &&
        bg_gradient_type.value
      )
    })

    // Background Preview
    const backgroundPreview = computed(() => {
      if (bg_selection.value === 'Single Color / Image') {
        return {
          backgroundColor: bg_backgroundColor.value,
          backgroundImage: `url(${fileUrl.value})`,
          backgroundPosition: bg_image_position.value,
          backgroundSize: bg_image_size.value,
          backgroundRepeat: bg_image_repeat.value,
          backgroundAttachment: bg_image_attachment.value,
          backgroundOrigin: bg_image_origin.value,
          backgroundClip: bg_image_clip.value,
        }
      } else {
        if (bg_gradient_type.value === 'linear-gradient') {
          return {
            background: `${bg_gradient_type.value}(${bg_gradient_angle.value}deg, ${bg_gradient_color_1.value} ${bg_gradient_position_1.value}%, ${bg_gradient_color_2.value} ${bg_gradient_position_2.value}%)`,
          }
        } else if (bg_gradient_type.value === 'radial-gradient') {
          return {
            background: `${bg_gradient_type.value}(${bg_gradient_color_1.value} ${bg_gradient_position_1.value}%, ${bg_gradient_color_2.value} ${bg_gradient_position_2.value}%)`,
          }
        } else {
          return ''
        }
      }
    })
    // Background Code
    const backgroundCode = computed(() => {
      let code = ''

      if (bg_selection.value === 'Single Color / Image') {
        if (bg_backgroundColor.value) {
          code += `background-color: ${bg_backgroundColor.value};\n`
        }
        if (fileUrl.value) {
          code += `background-image: url('${fileUrl.value}');\n`
        }
        if (bg_image_position.value) {
          code += `background-position: ${bg_image_position.value};\n`
        }
        if (bg_image_size.value) {
          code += `background-size: ${bg_image_size.value};\n`
        }
        if (bg_image_repeat.value) {
          code += `background-repeat: ${bg_image_repeat.value};\n`
        }
        if (bg_image_attachment.value) {
          code += `background-attachment: ${bg_image_attachment.value};\n`
        }
        if (bg_image_origin.value) {
          code += `background-origin: ${bg_image_origin.value};\n`
        }
        if (bg_image_clip.value) {
          code += `background-clip: ${bg_image_clip.value};\n`
        }
      } else if (bg_selection.value === 'Gradient Color') {
        if (bg_gradient_type.value === 'linear-gradient' && isLinear.value) {
          code += `background: ${bg_gradient_type.value}(${bg_gradient_angle.value}deg, ${bg_gradient_color_1.value} ${bg_gradient_position_1.value}%, ${bg_gradient_color_2.value} ${bg_gradient_position_2.value}%);\n`
        } else if (bg_gradient_type.value === 'radial-gradient' && isRadial.value) {
          code += `background: ${bg_gradient_type.value}(${bg_gradient_color_1.value} ${bg_gradient_position_1.value}%, ${bg_gradient_color_2.value} ${bg_gradient_position_2.value}%);\n`
        }
      }

      return code
    })

    // Emit(Send Data to parent)
    watch(backgroundCode, (newValue) => {
      ctx.emit('backgroundEmit', {
        type: 'background',
        code: newValue,
      })
    })

    //Props(Get Data From parent )
    const parseGradientString = (gradientString) => {
      const gradientParts = gradientString.match(/(linear-gradient|radial-gradient)\(([^)]+)\)/)
      if (gradientParts) {
        const type = gradientParts[1]
        const values = gradientParts[2].split(',')

        // Update gradient type
        bg_gradient_type.value = type

        // Assuming the first value is the angle for linear-gradient
        if (type === 'linear-gradient') {
          const angle = values.shift().trim()
          bg_gradient_angle.value = angle.match(/(\d+)deg/)[1]
        }

        // Update color stops
        if (values.length >= 2) {
          const colorStop1 = values[0].trim().split(' ')
          bg_gradient_color_1.value = colorStop1[0]
          bg_gradient_position_1.value = colorStop1[1].replace('%', '')

          const colorStop2 = values[1].trim().split(' ')
          bg_gradient_color_2.value = colorStop2[0]
          bg_gradient_position_2.value = colorStop2[1].replace('%', '')
        }
      }
    }
    Object.entries(props.backgroundProp).forEach(([key, value]) => {
      switch (key) {
        case 'background-color':
          bg_backgroundColor.value = value
          break
        case 'background-image':
          if (value instanceof File) {
            bg_imageFile.value = value
            handleUpload()
          }
          break
        case 'background-position':
          bg_image_position.value = value
          break
        case 'background-size':
          bg_image_size.value = value
          break
        case 'background-repeat':
          bg_image_repeat.value = value
          break
        case 'background-attachment':
          bg_image_attachment.value = value
          break
        case 'background-origin':
          bg_image_origin.value = value
          break
        case 'background-clip':
          bg_image_clip.value = value
          break
        case 'background':
          parseGradientString(value)
          break
        default:
          break
      }
    })
    onMounted(() => {
      if (isSingleColor.value) {
        bg_selection.value = 'Single Color / Image'
      } else if (isLinear.value || isRadial.value) {
        bg_selection.value = 'Gradient Color'
      }
    })
    //Clear Style Btn
    const clearObjItem = () => {
      bg_backgroundColor.value = ''
      bg_gradient_color_1.value = ''
      bg_gradient_color_2.value = ''
      bg_gradient_position_1.value = ''
      bg_gradient_position_2.value = ''
      bg_gradient_angle.value = ''
      bg_gradient_type.value = ''
      bg_gradient_option.value = ''
      bg_imageFile.value = ''
      fileUrl.value = ''
      bg_image_position.value = ''
      bg_image_size.value = ''
      bg_image_repeat.value = ''
      bg_image_attachment.value = ''
      bg_image_origin.value = ''
      bg_image_clip.value = ''
    }

    return {
      colorPalette,
      backgroundPreview,
      backgroundCode,
      bg_selection,
      bg_selection_options,
      bg_backgroundColor,
      bg_gradient_color_1,
      bg_gradient_color_2,
      bg_gradient_position_1,
      bg_gradient_position_2,
      bg_gradient_angle,
      bg_gradient_type,
      bg_gradient_types,
      bg_gradient_options,
      bg_gradient_option,
      bg_imageFile,
      fileUrl,
      handleUpload,
      isEmpty,
      bg_image_position,
      bg_image_positions,
      bg_image_size,
      bg_image_sizes,
      bg_image_repeat,
      bg_image_repeats,
      bg_image_attachment,
      bg_image_attachments,
      bg_image_origin,
      bg_image_origins,
      bg_image_clip,
      bg_image_clips,
      clearObjItem,
    }
  },
  components: {
    SubHeader,
  },
}
</script>

<style scoped></style>
