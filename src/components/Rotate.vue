<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Rotate" :onClear="clearObjItem" />
  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="rotate_type"
          :options="rotate_types"
          label="Type"
          class="mb-10"
        />
        <div v-if="rotate_type == '2D'">
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Angle</span><span>{{ rotate_angle }} deg </span>
            </div>
            <q-slider
              v-model="rotate_angle"
              track-size="5px"
              inner-track-color="primary"
              thumb-size="15px"
              :min="0"
              :max="360"
              class="mb-10"
            ></q-slider>
          </div>
        </div>
        <div v-if="rotate_type == '3D'">
          <div class="outlined-slider mb-10">
            <div class="slider-label">
              <span>Angle X</span><span>{{ rotate_angle_x }} deg </span>
            </div>
            <q-slider
              v-model="rotate_angle_x"
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
              <span>Angle Y</span><span>{{ rotate_angle_y }} deg </span>
            </div>
            <q-slider
              v-model="rotate_angle_y"
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
              <span>Angle Z</span><span>{{ rotate_angle_z }} deg </span>
            </div>
            <q-slider
              v-model="rotate_angle_z"
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
    </div>
    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box">
        <div class="rotate-preview" :style="rotatePreview">
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nisi cum
          voluptas autem officiis suscipit eius distinctio, porro quibusdam
          dolore quae saepe ipsum iste necessitatibus sunt quisquam rerum, unde
          vel eveniet impedit ratione soluta recusandae? Voluptas dolor ipsam
          aspernatur excepturi porro!
        </div>
      </div>
      <div class="code-box">
        {{ rotateCode }}
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["rotateEmit"],
  props: {
    rotateProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const rotate_type = ref("2D");
    const rotate_types = ["2D", "3D"];

    // Initialize numeric refs
    const rotate_angle = ref();
    const rotate_angle_x = ref();
    const rotate_angle_y = ref();
    const rotate_angle_z = ref();
    const is3D = computed(() => {
      return (
        rotate_angle_x.value !== "" &&
        rotate_angle_y.value !== "" &&
        rotate_angle_z.value !== "" &&
        rotate_angle_x.value !== undefined &&
        rotate_angle_y.value !== undefined &&
        rotate_angle_z.value !== undefined
      );
    });
    const rotatePreview = computed(() => {
      return rotate_type.value === "2D"
        ? { transform: `rotate(${rotate_angle.value}deg)` }
        : {
            transform: `rotateX(${rotate_angle_x.value}deg) rotateY(${rotate_angle_y.value}deg) rotateZ(${rotate_angle_z.value}deg)`,
          };
    });

    const rotateCode = computed(() => {
      if (rotate_angle.value !== "" && rotate_angle.value !== undefined) {
        return `transform: rotate(${rotate_angle.value}deg);\n`;
      } else if (is3D.value) {
        return `transform: rotateX(${rotate_angle_x.value}deg) rotateY(${rotate_angle_y.value}deg) rotateZ(${rotate_angle_z.value}deg);\n`;
      } else return "";
    });
    watch(rotateCode, (newVal) => {
      ctx.emit("rotateEmit", {
        type: "rotate",
        code: newVal,
      });
    });

    // Function to parse and convert string values to numbers
    const parseRotateProp = () => {
      if (props.rotateProp.transform) {
        const transform = props.rotateProp.transform;
        const rotate2DMatch = transform.match(/rotate\((\d+)deg\)/);
        const rotate3DMatch = transform.match(
          /rotateX\((\d+)deg\) rotateY\((\d+)deg\) rotateZ\((\d+)deg\)/
        );

        if (rotate2DMatch) {
          rotate_type.value = "2D";
          rotate_angle.value = Number(rotate2DMatch[1]);
        } else if (rotate3DMatch) {
          rotate_type.value = "3D";
          rotate_angle_x.value = Number(rotate3DMatch[1]);
          rotate_angle_y.value = Number(rotate3DMatch[2]);
          rotate_angle_z.value = Number(rotate3DMatch[3]);
        }
      }
    };
    onMounted(() => {
      if (rotate_angle.value) {
        rotate_type.value = "2D";
      } else if (is3D.value) {
        rotate_type.value = "3D";
      }
    });

    onMounted(() => {
      parseRotateProp();
    });

    const clearObjItem = () => {
      rotate_angle.value = "";
      rotate_angle_x.value = "";
      rotate_angle_y.value = "";
      rotate_angle_z.value = "";
      rotatePreview.value.transform = "";
    };

    return {
      rotatePreview,
      rotateCode,
      rotate_type,
      rotate_types,
      rotate_angle,
      rotate_angle_x,
      rotate_angle_y,
      rotate_angle_z,
      clearObjItem,
    };
  },

  components: {
    SubHeader,
  },
};
</script>

<style scoped>
.rotate-preview {
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
