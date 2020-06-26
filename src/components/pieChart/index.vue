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
var _self;
var canvaPie = null;

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
    header: String,
    width: Number,
    height: Number,
    id: String,
    options: Object || undefined
  },
  mounted() {
    _self = this;
    const { initData, width, height, header, id } = _self.$props;

    this.style = {
      width: `100%`,
      height: `${height * _self.pixelRatio}upx`
    };
    this.cWidth = uni.upx2px(width - 40);
    this.cHeight = uni.upx2px(height);

    if (initData) {
      _self.showPie(id, initData);
    }
  },
  methods: {
    showPie(canvasId, chartData) {
      canvaPie = new uCharts({
        $this: _self,
        canvasId: canvasId,
        type: "pie",
        fontSize: 11,
        legend: { show: true, fontColor: "#59595f" },
        pixelRatio: _self.pixelRatio,
        series: chartData.series,
        animation: true,
        width: _self.cWidth * _self.pixelRatio,
        height: _self.cHeight * _self.pixelRatio,
        dataLabel: true,
        extra: {
          pie: {
            lableWidth: 15
          }
        },
        ..._self.$props.options
      });
    },
    touchPie(e) {
      canvaPie.showToolTip(e, {
        format: function(item) {
          return item.name + ": " + item.data;
        }
      });
    }
  }
};
</script>

<style>
</style>