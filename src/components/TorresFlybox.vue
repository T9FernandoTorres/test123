<template>
  <div class="torres-flybox" :ref="refName">
    <svg :width="width" :height="height">
      <defs>
        <path :id="pathId" :d="path" fill="none" />
        <radialGradient
          :id="radialGradientId"
          fx="50%"
          fy="50%"
          cx="50%"
          cy="50%"
          r="50%"
        >
          <!-- radialGradient fx决定光源的起始位置 -->
          <stop offset="0%" stop-color="#fff" stop-opacity="1" />
          <stop offset="100%" stop-color="#fff" stop-opacity="0" />
        </radialGradient>
        <mask :id="maskId">
          <circle
            :r="starLength"
            cx="0"
            cy="0"
            :fill="`url(#${radialGradientId})`"
          >
            <!-- circle r控制流星的长度 -->
            <animateMotion
              :path="path"
              :dur="`${duration}s`"
              rotate="auto"
              repeatCount="indefinite"
            ></animateMotion>
          </circle>
        </mask>
      </defs>
      <use :href="`#${pathId}`" stroke-width="1" :stroke="lineColor" />
      <use
        :href="`#${pathId}`"
        stroke-width="3"
        :stroke="starColor"
        :mask="`url(#${maskId})`"
      />
    </svg>
    <div class="torres-flybox-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, getCurrentInstance, computed } from "vue";
import { v4 as uuidv4 } from "uuid";
export default {
  props: {
    lineColor: {
      type: String,
      default: "#235fa7",
    },
    starColor: {
      type: String,
      default: "#4fd2dd",
    },
    starLength: {
      type: [String, Number],
      default: 64,
    },
    duration: {
      type: [Number, String],
      default: 3,
    },
  },
  setup() {
    const uuid = uuidv4();
    console.log(uuid);
    const width = ref(0);
    const height = ref(0);
    const refName = "torresFlybox";
    const pathId = `${refName}-path${uuid}`;
    const maskId = `${refName}-mask${uuid}`;
    const radialGradientId = `${refName}-radialGradient${uuid}`;
    const path = computed(
      () =>
        `M5 5 L${width.value - 5} 5 L${width.value - 5} ${
          height.value - 5
        } L5 ${height.value - 5} Z`
    );

    const init = () => {
      //拿到父容器的dom
      const instance = getCurrentInstance();
      const dom = instance.ctx.$refs[refName];
      width.value = dom.clientWidth;
      height.value = dom.clientHeight;
    };
    onMounted(() => {
      init();
    });
    return {
      width,
      height,
      refName,
      path,
      pathId,
      maskId,
      radialGradientId,
    };
  },
};
</script>

<style lang="scss" scoped>
.torres-flybox {
  position: relative;
  width: 100%;
  height: 100%;
  svg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  .torres-flybox-content {
    width: 100%;
    height: 100%;
    padding: 5px;
    box-sizing: border-box;
  }
}
</style>