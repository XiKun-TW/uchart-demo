<template>
  <view>
    <view v-if="header" class="chart-header">{{ header }}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        v-bind:style="style"
        class="charts"
        @touchstart="touchRadar"
      ></canvas>
    </view>
  </view>
</template>

<script>
import uCharts from "@/uCharts/u-charts.js";

export default {
  data() {
    return {
      cWidth: "",
      cHeight: "",
      pixelRatio: 1,
      style: {}
    };
  },
  props: {
    initData: Object,
    width: Number,
    height: Number,
    header: String,
    id: String,
    options: Object || undefined
  },
  mounted() {
    const { initData, width, height, id } = this.$props;

    this.style = {
      width: `${(width - 40) * this.pixelRatio}upx`,
      height: `${height * this.pixelRatio}upx`
    };
    this.cWidth = uni.upx2px(width - 40);
    this.cHeight = uni.upx2px(height);

    if (initData) {
      this.showRadar(id, initData);
    }
  },
  methods: {
    showRadar(canvasId, chartData) {
      this.canvaRadar = new uCharts({
        $this: this,
        canvasId: canvasId,
        type: "radar",
        fontSize: 11,
        legend: { show: true },
        background: "#FFFFFF",
        pixelRatio: this.pixelRatio,
        animation: true,
        dataLabel: true,
        categories: chartData.categories,
        series: chartData.series,
        width: this.cWidth * this.pixelRatio,
        height: this.cHeight * this.pixelRatio,
        ...this.$props.options
      });
    },
    touchRadar(e) {
      this.canvaRadar.showToolTip(e, {
        format: item => {
          return `${item.name}: ${item.data}%`;
        }
      });
    }
  }
};
</script>

<style>
</style>
