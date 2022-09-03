<template>
  <div class="home">
    <torres-loading v-if="loading">
      <div class="loading-text">数据大屏加载中...</div>
    </torres-loading>
    <torres-container :options="{ width: 3840, height: 2160 }" v-else>
      <div class="header">
        <top-header />
      </div>
      <div class="separator"></div>
      <div class="center">
        <div class="left">
          <div class="left1">
            <total-users
              :today-user="todayUser"
              :growth-lastDay="growthLastDay"
              :growth-lastMonth="growthLastMonth"
            />
          </div>
          <div class="left2">
            <average-age :data="ageData" :avg-age="averageAge" />
          </div>
          <div class="left3">
            <total-device :data="deviceData" />
          </div>
          <div class="left4">
            <total-gender :data="genderData" />
          </div>
          <div class="left5">
            <total-rider :data="riderData" />
          </div>
          <div class="left6">
            <hot-category :data="hotCategoryData" />
          </div>
        </div>
        <div class="right">
          <div class="right-top1">
            <center-header :data="headerData" />
          </div>
          <div class="right-top2">
            <transform-category
              :data="['北京', '上海', '广州', '深圳', '成都', '杭州', '南京']"
            />
          </div>
          <div class="right-bottom">
            <div class="right-bottom-left">
              <div class="right-bottom-left1">
                <!-- <gdp-timeline-chart/> -->
                <!-- <map-test /> -->
                <rotating-earth />
              </div>
              <div class="right-bottom-left2">
                <transform-category
                  :data="['订单量', '销售额', '用户数', '退单量']"
                  :color="['rgb(178,209,126)', 'rgb(116,166,49)']"
                />
              </div>
              <div class="right-bottom-left3">1111</div>
              <div class="right-bottom-left4">1111</div>
            </div>
            <div class="right-bottom-right">
              <div class="right-bottom-right1">
                <sales-list :data="salesListData" />
              </div>
              <div class="right-bottom-right2">1111</div>
            </div>
          </div>
        </div>
      </div>
    </torres-container>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import useScreenData from "../hooks/useScreenData";

import TorresContainer from "../components/TorresContainer.vue";
import TorresLoading from "../components/TorresLoading.vue";
import TopHeader from "../components/TopHeader.vue";
import TotalUsers from "@/components/TotalUsers.vue";
import AverageAge from "@/components/AverageAge.vue";
import TotalDevice from "@/components/TotalDevice.vue";
import TotalGender from "@/components/TotalGender.vue";
import TotalRider from "@/components/TotalRider.vue";
import HotCategory from "@/components/HotCategory.vue";
import CenterHeader from "@/components/CenterHeader.vue";
import TransformCategory from "@/components/TransformCategory.vue";
import SalesList from "@/components/SalesList.vue";
// import MapTest from '@/components/MapTest.vue';
import RotatingEarth from '@/components/RotatingEarth.vue';
// import GdpTimelineChart from '@/components/GdpTimelineChart.vue';

export default {
  components: {
    TorresContainer,
    TorresLoading,
    TopHeader,
    TotalUsers,
    AverageAge,
    TotalDevice,
    TotalGender,
    TotalRider,
    HotCategory,
    CenterHeader,
    TransformCategory,
    SalesList,
    // MapTest,
    RotatingEarth,
    // GdpTimelineChart,
  },
  setup() {
    const loading = ref(true);

    onMounted(() => {
      setTimeout(() => {
        loading.value = false;
      }, 3000);
    });
    return {
      loading,
      ...useScreenData(),
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgb(29, 29, 29);
  color: #fff;
  font-size: 48px;
  #torres-container {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .header {
      width: 100%;
      height: 167px;
      background: yellowgreen;
    }
    .separator {
      width: 100%;
      height: 10px;
      background: rgb(92, 88, 89);
    }
    .center {
      width: 100%;
      display: flex;
      flex: 1;
      background: rgb(92, 88, 89);
      .left {
        flex: 0 0 860px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 860px;
        height: 100%;
        padding-bottom: 20px;
        box-sizing: border-box;
        .left1 {
          height: 300px;
        }
        .left2 {
          height: 320px;
        }
        .left3 {
          height: 280px;
        }
        .left4 {
          height: 230px;
        }
        .left5 {
          height: 360px;
        }
        .left6 {
          height: 360px;
        }
      }
      .right {
        flex: 1;
        display: flex;
        flex-direction: column;
        margin-left: 10px;
        .right-top1 {
          width: 100%;
          height: 206px;
        }
        .right-top2 {
          width: 100%;
          height: 48px;
          margin: 10px 0;
        }
        .right-bottom {
          flex: 1;
          display: flex;
          padding-bottom: 20px;
          .right-bottom-left {
            flex: 0 0 1917px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            width: 1917px;
            .right-bottom-left1 {
              height: 999px;
              background: paleturquoise;
            }
            .right-bottom-left2 {
              height: 80px;
            }
            .right-bottom-left3 {
              height: 350px;
              background: red;
            }
            .right-bottom-left4 {
              height: 220px;
              background: papayawhip;
            }
          }
          .right-bottom-right {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            margin-left: 10px;
            .right-bottom-right1 {
              width: 100%;
              height: 999px;
              margin-left: 20px;
            }
            .right-bottom-right2 {
              margin-top: 10px;
              flex: 1;
              width: 100%;
              background-color: #333;
            }
          }
        }
      }
    }
  }
}
.loading-text {
  font-size: 20px;
  margin-top: 15px;
}
</style>