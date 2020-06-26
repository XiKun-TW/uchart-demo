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
var _self;
var canvaRadar = null;

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
      _self.showRadar(id, initData);
    }
  },
  methods: {
    showRadar(canvasId, chartData) {
      canvaRadar = new uCharts({
        $this: _self,
        canvasId: canvasId,
        type: "radar",
        fontSize: 11,
        legend: { show: true },
        background: "#FFFFFF",
        pixelRatio: _self.pixelRatio,
        animation: true,
        dataLabel: true,
        categories: chartData.categories,
        series: chartData.series,
        width: _self.cWidth * _self.pixelRatio,
        height: _self.cHeight * _self.pixelRatio,
        ..._self.$props.options
      });
    },
    touchRadar(e) {
      canvaRadar.showToolTip(e, {
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
