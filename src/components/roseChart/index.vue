<template>
  <view>
    <view v-if="header" class="chart-header">{{ header }}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        v-bind:style="style"
        class="charts"
        @touchstart="touchPie"
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
      this.showPie(id, initData);
    }
  },
  methods: {
    showPie(canvasId, chartData) {
      this.canvaPie = new uCharts({
        $this: this,
        canvasId: canvasId,
        type: "rose",
        fontSize: 11,
        legend: { show: true },
        background: "#FFFFFF",
        pixelRatio: this.pixelRatio,
        series: chartData.series,
        animation: true,
        width: this.cWidth * this.pixelRatio,
        height: this.cHeight * this.pixelRatio,
        dataLabel: true,
        extra: {
          rose: {
            type: "area",
            minRadius: 50,
            activeOpacity: 0.5,
            offsetAngle: 0,
            labelWidth: 15
          }
        },
        ...this.$props.options
      });
    },
    touchPie(e) {
      this.canvaPie.showToolTip(e, {
        format: function(item) {
          return item.name + ":" + item.data;
        }
      });
    }
  }
};
</script>

<style>
</style>