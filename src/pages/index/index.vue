<template>
  <view class="body">
    <view class="chart-container">
      <line-chart
        header="线型图"
        id="lineChart"
        v-bind:initData="lineMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></line-chart>
    </view>
    <view class="chart-container">
      <pie-chart
        header="饼状图"
        id="pieChart"
        v-bind:initData="pieMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></pie-chart>
    </view>
    <view class="chart-container">
      <donut-chart
        header="环状图"
        id="ringChart"
        v-bind:initData="donutMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></donut-chart>
    </view>
    <view class="chart-container">
      <column-chart
        header="柱状图"
        id="columnChart"
        v-bind:initData="columnMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></column-chart>
    </view>
    <view class="chart-container">
      <column-chart
        header="柱状图(横向)"
        id="columnRotateChart"
        rotate
        v-bind:initData="columnMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></column-chart>
    </view>
    <view class="chart-container">
      <area-chart
        header="区域图"
        id="areaChart"
        v-bind:initData="areaMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></area-chart>
    </view>
    <view class="chart-container">
      <radar-chart
        header="雷达图"
        id="radarChart"
        v-bind:initData="radarMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></radar-chart>
    </view>
    <view class="chart-container">
      <funnel-chart
        header="漏斗图"
        id="funnelChart"
        v-bind:initData="funnelMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></funnel-chart>
    </view>
    <view class="chart-container">
      <rose-chart
        header="玫瑰图"
        id="roseChart"
        v-bind:initData="roseMockData"
        v-bind:width="750"
        v-bind:height="500"
      ></rose-chart>
    </view>
  </view>
</template>

<script lang="ts">
import Vue from "vue";
import lineChart from "@/components/lineChart/index.vue";
import pieChart from "@/components/pieChart/index.vue";
import donutChart from "@/components/donutChart/index.vue";
import columnChart from "@/components/columChart/index.vue";
import areaChart from "@/components/areaChart/index.vue";
import radarChart from "@/components/radarChart/index.vue";
import funnelChart from "@/components/funnelChart/index.vue";
import roseChart from "@/components/roseChart/index.vue";
import mockData from "@/constants/mockData";

export default Vue.extend({
  data() {
    return {
      title: "Hello",
      lineMockData: mockData.data.LineA,
      pieMockData: mockData.data.Pie,
      donutMockData: mockData.data.Ring,
      columnMockData: mockData.data.Column,
      areaMockData: mockData.data.Area,
      radarMockData: mockData.data.Radar,
      funnelMockData: mockData.data.Funnel,
      roseMockData: mockData.data.Pie
    };
  },
  onLoad() {},
  methods: {},
  components: {
    "line-chart": lineChart,
    "pie-chart": pieChart,
    "donut-chart": donutChart,
    "column-chart": columnChart,
    "area-chart": areaChart,
    "radar-chart": radarChart,
    "funnel-chart": funnelChart,
    "rose-chart": roseChart
  }
});
</script>

<style>
</style>
