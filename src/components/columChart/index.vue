<template>
  <view>
    <view v-if="header" class="chart-header">{{header}}</view>
    <view class="chart-canvas">
      <canvas
        v-bind:canvas-id="id"
        v-bind:id="id"
        v-bind:style="style"
        class="charts"
        @touchstart="touchColumn"
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
      style: {},
      canvas: null
    };
  },
  props: {
    initData: Object,
    width: Number,
    height: Number,
    header: String,
    rotate: false,
    id: String,
    options: Object
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
      this.showColumn(id, initData);
    }
  },
  methods: {
    showColumn(canvasId, chartData) {
      const { rotate } = this.$props;
      this.canvas = new uCharts({
        $this: this,
        canvasId: canvasId,
        type: "column",
        legend: { show: true },
        fontSize: 11,
        background: "#FFFFFF",
        pixelRatio: this.pixelRatio,
        animation: true,
        rotate: !!rotate,
        categories: chartData.categories,
        series: chartData.series,
        xAxis: {
          disableGrid: true
        },
        yAxis: {
          //disabled:true
        },
        dataLabel: true,
        width: this.cWidth * this.pixelRatio,
        height: this.cHeight * this.pixelRatio,
        extra: {
          column: {
            type: "group",
            width:
              (this.cWidth * this.pixelRatio * 0.45) /
              chartData.categories.length
          }
        },
        ...this.$props.options
      });
    },
    touchColumn(e) {
      this.canvas.showToolTip(e, {
        format: function(item, category) {
          if (typeof item.data === "object") {
            return category + " " + item.name + ":" + item.data.value;
          } else {
            return category + " " + item.name + ":" + item.data;
          }
        }
      });
    }
  }
};
</script>
<style>
</style>
