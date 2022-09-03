<template>
  <div class="earth-wrapper">
    <vue-echarts :options="options" />
  </div>
</template>

<script>
import 'echarts-gl';
import { ref, onMounted } from "vue";
import VueEcharts from "./VueEcharts/VueEcharts.vue";

const ROOT_PATH = "./";

export default {
  components: { VueEcharts },
  setup() {
    const options = ref({});
    const update = () => {
      options.value = {
        backgroundColor: "#000",
        globe: {
          baseTexture: `${ROOT_PATH}assets/datav-gl-texture.jpg`, //纹理贴图
          //高度纹理贴图
          heightTexture: `${ROOT_PATH}assets/datav-gl-texture.jpg`,
          displacementScale: 0.04, //使地球更加立体
          shading: "realistic", //让地球更加真实感渲染
          environment: `${ROOT_PATH}assets/star-bg.jpg`, //背景环境贴图
          realisticMaterial: {
            roughness: 0.9,//粗糙度 0.1-1取值
          },
          postEffect: {
            enable: true,
          },
          light: {
            main: {
              intensity: 5,
              shadow: true,
            },
            ambientCubemap: {
              texture: `${ROOT_PATH}assets/pisa.hdr`,
              diffuseIntensity: 0.2,
            },
          },
        },
      };
    };
    onMounted(update);
    return {
      options,
    };
  },
};
</script>

<style lang="scss" scoped>
.earth-wrapper {
  width: 100%;
  height: 100%;
}
</style>