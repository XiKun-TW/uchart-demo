<template>
  <view>
    <view v-if="header" class="chart-header">{{ header }}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        v-bind:style="style"
        class="charts"
        @touchstart="touchArea"
      ></canvas>
    </view>
  </view>
</template>

<script>
import uCharts from "@/uCharts/u-charts.js";
var _self;
var canvaFunnel = null;

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
    _self = this;

    const { initData, width, height, id } = _self.$props;

    this.style = {
      width: `${(width - 40) * _self.pixelRatio}upx`,
      height: `${height * _self.pixelRatio}upx`
    };
    this.cWidth = uni.upx2px(width - 40);
    this.cHeight = uni.upx2px(height);

    if (initData) {
      _self.showFunnel(id, initData);
    }
  },
  methods: {
    showFunnel(canvasId, chartData) {
      canvaFunnel = new uCharts({
        $this: this,
        canvasId: canvasId,
        type: "funnel",
        fontSize: 11,
        padding: [15, 15, 0, 15],
        legend: {
          show: true,
          padding: 5,
          lineHeight: 11,
          margin: 5
        },
        background: "#FFFFFF",
        pixelRatio: this.pixelRatio,
        series: chartData.series,
        animation: true,
        width: this.cWidth * this.pixelRatio,
        height: this.cHeight * this.pixelRatio,
        dataLabel: true,
        ..._self.$props.options
      });
    },
    touchArea(e) {
      canvaFunnel.showToolTip(e, {
        format: function(item, category) {
          return item.name + ":" + item.data;
        }
      });
    }
  }
};
</script>

<style>
</style>
