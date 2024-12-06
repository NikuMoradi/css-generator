<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <SubHeader title="Position" :onClear="clearObjItem" />

  <div class="row" style="justify-content: space-between">
    <div class="col-xs-12 col-sm-12 col-md-6">
      <div class="no-scroll-area">
        <q-select
          outlined
          v-model="position_position"
          :options="position_positions"
          label="Value"
          class="mb-10"
        />
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="position_top"
              label="Top"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="position_top_unitType"
              :options="position_top_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="position_right"
              label="Right"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="position_right_unitType"
              :options="position_right_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="position_bottom"
              label="Bottom"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="position_bottom_unitType"
              :options="position_bottom_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="position_left"
              label="Left"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
          <div class="col-6">
            <q-select
              outlined
              v-model="position_left_unitType"
              :options="position_left_unitTypes"
              label="Unit"
              class="mb-10"
            />
          </div>
        </div>
        <div class="row q-col-gutter-sm">
          <div class="col-6">
            <q-input
              v-model.number="position_zIndex"
              label="Z-index"
              type="number"
              outlined
              class="mb-10"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="col-sm-12 col-md-5 q-gutter-y-lg" v-if="$q.screen.gt.sm">
      <div class="preview-box"></div>
      <div class="code-box">
        <q-scroll-area style="height: 4rem"> {{ positionCode }}</q-scroll-area>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, computed, watch, onMounted } from "vue";
import SubHeader from "./SubHeader.vue";

export default {
  emits: ["positionEmit"],
  props: {
    positionProp: {
      type: Object,
      required: false,
    },
  },
  setup(props, ctx) {
    const position_position = ref("");
    const position_positions = [
      "",
      "static",
      "absolute",
      "fixed",
      "relative",
      "sticky",
    ];
    const position_top = ref("");
    const position_right = ref("");
    const position_bottom = ref("");
    const position_left = ref("");
    const position_top_unitType = ref("");
    const position_top_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const position_right_unitType = ref("");
    const position_right_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const position_bottom_unitType = ref("");
    const position_bottom_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const position_left_unitType = ref("");
    const position_left_unitTypes = [
      "",
      "px",
      "%",
      "em",
      "rem",
      "vw",
      "vh",
      "vmin",
      "vmax",
      "cm",
      "mm",
      "pt",
      "pc",
      "ex",
      "ch",
      "in",
    ];
    const position_zIndex = ref("");
    // const positionPreview = computed(() => {
    //   return {
    //     position: `${position_position.value}`,
    //     top: `${position_top.value}${position_top_unitType.value}`,
    //     right: `${position_right.value}${position_right_unitType.value}`,
    //     bottom: `${position_bottom.value}${position_bottom_unitType.value}`,
    //     left: `${position_left.value}${position_left_unitType.value}`,
    //     zIndex: `${position_zIndex.value}`,
    //   };
    // });
    const positionCode = computed(() => {
      let code = "";
      if (position_position.value) {
        code += `position: ${position_position.value};\n`;
      }
      if (position_top.value && position_top_unitType.value) {
        code += `top: ${position_top.value}${position_top_unitType.value};\n`;
      }
      if (position_right.value && position_right_unitType.value) {
        code += `right: ${position_right.value}${position_right_unitType.value};\n`;
      }
      if (position_bottom.value && position_bottom_unitType.value) {
        code += `bottom: ${position_bottom.value}${position_bottom_unitType.value};\n`;
      }
      if (position_left.value && position_left_unitType.value) {
        code += `left: ${position_left.value}${position_left_unitType.value};\n`;
      }
      if (position_zIndex.value) {
        code += `z-index: ${position_zIndex.value};\n`;
      }
      return code;
    });

    watch(positionCode, (newVal) => {
      ctx.emit("positionEmit", { type: "position", code: newVal });
    });
    const parseValueAndUnit = (value) => {
      const match = value.match(/^(\d+)([a-z%]*)$/);
      return match ? [match[1], match[2]] : [value, ""];
    };

    const parsePositionProp = () => {
      if (props.positionProp) {
        if (props.positionProp.position) {
          position_position.value = props.positionProp.position;
        }
        if (props.positionProp.top) {
          const [value, unit] = parseValueAndUnit(props.positionProp.top);
          position_top.value = value;
          position_top_unitType.value = unit;
        }
        if (props.positionProp.right) {
          const [value, unit] = parseValueAndUnit(props.positionProp.right);
          position_right.value = value;
          position_right_unitType.value = unit;
        }
        if (props.positionProp.bottom) {
          const [value, unit] = parseValueAndUnit(props.positionProp.bottom);
          position_bottom.value = value;
          position_bottom_unitType.value = unit;
        }
        if (props.positionProp.left) {
          const [value, unit] = parseValueAndUnit(props.positionProp.left);
          position_left.value = value;
          position_left_unitType.value = unit;
        }
        if (props.positionProp["z-index"]) {
          position_zIndex.value = props.positionProp["z-index"];
        }
      }
    };

    onMounted(() => {
      parsePositionProp();
    });

    const clearObjItem = () => {
      position_position.value = "";
      position_top.value = "";
      position_right.value = "";
      position_bottom.value = "";
      position_left.value = "";
      position_top_unitType.value = "";
      position_right_unitType.value = "";
      position_bottom_unitType.value = "";
      position_left_unitType.value = "";
      position_zIndex.value = "";
    };

    return {
      // positionPreview,
      positionCode,
      position_position,
      position_positions,
      position_top,
      position_right,
      position_bottom,
      position_left,
      position_top_unitType,
      position_top_unitTypes,
      position_right_unitType,
      position_right_unitTypes,
      position_bottom_unitType,
      position_bottom_unitTypes,
      position_left_unitType,
      position_left_unitTypes,
      position_zIndex,
      clearObjItem,
    };
  },
  components: {
    SubHeader,
  },
};
</script>

<style scoped></style>
