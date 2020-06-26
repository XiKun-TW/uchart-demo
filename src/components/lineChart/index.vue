<template>
  <view>
    <view v-if="header" class="chart-header">{{ header }}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        v-bind:style="style"
        class="charts"
        @touchstart="touchLineA"
      ></canvas>
    </view>
  </view>
</template>

<script>
import uCharts from "@/uCharts/u-charts.js";

var _self;
var canvaLineA = null;

const defaultyAxis = {
  gridType: "grid",
  gridColor: "#CCCCCC",
  dashLength: 8,
  splitNumber: 5
};

const defaultxAxis = {
  type: "grid",
  gridColor: "#CCCCCC",
  gridType: "dash",
  dashLength: 8
};

export default {
  data() {
    return {
      cWidth: "",
      cHeight: "",
      pixelRatio: 1,
      style: {}
    };
  },
  mounted() {
    _self = this;
    const { initData, width, height, id } = _self.$props;
    this.cWidth = uni.upx2px(width - 40);
    this.cHeight = uni.upx2px(height);
    this.style = {
      width: `${(width - 40) * _self.pixelRatio}upx`,
      height: `${height * _self.pixelRatio}upx`
    };

    if (initData) {
      _self.showLineA(id, initData);
    }
  },
  props: {
    initData: Object,
    width: Number,
    height: Number,
    header: String,
    id: String,
    xAxis: Object || undefined,
    yAxis: Object || undefined,
    options: Object || undefined
  },
  methods: {
    showLineA(canvasId, chartData) {
      canvaLineA = new uCharts({
        $this: _self,
        canvasId: canvasId,
        type: "line",
        fontSize: 12,
        legend: { show: true, fontColor: "#59595f" },
        dataLabel: false,
        dataPointShape: true,
        pixelRatio: _self.pixelRatio,
        categories: chartData.categories,
        series: chartData.series,
        animation: true,
        xAxis: {
          ...defaultxAxis,
          ..._self.$props.xAxis
        },
        yAxis: {
          ...defaultyAxis,
          ..._self.$props.yAxis
        },
        width: _self.cWidth * _self.pixelRatio,
        height: _self.cHeight * _self.pixelRatio,
        extra: {
          line: {
            type: "curve"
          }
        },
        ..._self.$props.options
      });
    },
    touchLineA(e) {
      canvaLineA.showToolTip(e, {
        format: function(item, category) {
          return category + " " + item.name + ":" + item.data;
        }
      });
    }
  }
};
</script>

<style>
</style>
