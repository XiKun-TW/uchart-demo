<template>
  <view>
    <view v-if="header" class="chart-header">{{ header }}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        class="charts"
        v-bind:style="style"
        @touchstart="touchRing"
      ></canvas>
    </view>
  </view>
</template>

<script>
import uCharts from "@/uCharts/u-charts.js";
var _self;
var canvaRing = null;

export default {
  data() {
    return {
      cWidth: "",
      cHeight: "",
      pixelRatio: 1,
      serverData: "",
      style: {}
    };
  },
  props: {
    initData: Object,
    width: Number,
    height: Number,
    header: String,
    id: String
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
      _self.showRing(id, initData);
    }
  },
  methods: {
    showRing(canvasId, chartData) {
      canvaRing = new uCharts({
        $this: _self,
        canvasId: canvasId,
        type: "ring",
        fontSize: 11,
        legend: { show: true, fontColor: "#59595f" },
        extra: {
          pie: {
            offsetAngle: -45,
            ringWidth: 40 * _self.pixelRatio,
            labelWidth: 15,
            borderColor: "#2b2d48"
          }
        },
        pixelRatio: _self.pixelRatio,
        series: chartData.series,
        animation: true,
        width: _self.cWidth * _self.pixelRatio,
        height: _self.cHeight * _self.pixelRatio,
        disablePieStroke: true,
        dataLabel: true
      });
    },
    touchRing(e) {
      canvaRing.showToolTip(e, {
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