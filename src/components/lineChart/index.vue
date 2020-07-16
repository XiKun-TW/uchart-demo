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
    const { initData, width, height, id } = this.$props;
    this.cWidth = uni.upx2px(width - 40);
    this.cHeight = uni.upx2px(height);
    this.style = {
      width: `${(width - 40) * this.pixelRatio}upx`,
      height: `${height * this.pixelRatio}upx`
    };

    if (initData) {
      this.showLineA(id, initData);
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
      this.canvaLineA = new uCharts({
        $this: this,
        canvasId: canvasId,
        type: "line",
        fontSize: 12,
        legend: { show: true, fontColor: "#59595f" },
        dataLabel: false,
        dataPointShape: true,
        pixelRatio: this.pixelRatio,
        categories: chartData.categories,
        series: chartData.series,
        animation: true,
        xAxis: {
          ...defaultxAxis,
          ...this.$props.xAxis
        },
        yAxis: {
          ...defaultyAxis,
          ...this.$props.yAxis
        },
        width: this.cWidth * this.pixelRatio,
        height: this.cHeight * this.pixelRatio,
        extra: {
          line: {
            type: "curve"
          }
        },
        ...this.$props.options
      });
    },
    touchLineA(e) {
      this.canvaLineA.showToolTip(e, {
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
