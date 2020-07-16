<template>
  <view class="body dark-theme">
    <view class="over-all">
      <view class="income">
        <view class="price">￥155（百万）</view>
        <view class="catgory">6月总收入</view>
      </view>
      <view class="stat">
        <view class="price">700（千）</view>
        <view class="catgory">6月总乘次</view>
      </view>
    </view>
    <view class="chart-container">
      <line-chart
        id="monthlyIncome"
        header="2020年收入趋势"
        v-bind:initData="monthlyIncomeData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:yAxis="yAxis"
        v-bind:options="lineOptions"
      ></line-chart>
    </view>
    <view class="chart-container">
      <line-chart
        id="yearlyIncome"
        header="18-20年收入同比对比"
        v-bind:initData="yearlyIncomeData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:yAxis="yAxis"
        v-bind:options="lineOptions"
      ></line-chart>
    </view>
    <view class="chart-container">
      <column-chart
        id="salesType"
        header="2020年销量月对比"
        v-bind:initData="salesData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="columnOptions"
      ></column-chart>
    </view>
    <view class="chart-container">
      <column-chart
        id="yearSalesType"
        header="2020年1-6月销量同比对比"
        v-bind:initData="yearSalesData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="yearColumnOptions"
      ></column-chart>
    </view>
    <view class="chart-container">
      <donut-chart
        id="incomeType"
        header="2020年6月收入类型占比"
        v-bind:initData="incomeType"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="pieOptions"
      ></donut-chart>
    </view>
    <view class="chart-container">
      <rose-chart
        id="roseType"
        header="2020年6月用户职业占比"
        v-bind:initData="customJobData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="roseOptions"
      ></rose-chart>
    </view>
    <view class="chart-container">
      <funnel-chart
        id="funnelType"
        header="2020年6月用户丢失率分析"
        v-bind:initData="lostData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="funnelOptions"
      ></funnel-chart>
    </view>
    <view class="chart-container">
      <radar-chart
        id="radarType"
        header="2020年(4-6月)用户类型分析"
        v-bind:initData="customTypeData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="radarOptions"
      ></radar-chart>
    </view>
  </view>
</template>
<script>
import Vue from "vue";
import lineChart from "@/components/lineChart/index.vue";
import pieChart from "@/components/pieChart/index.vue";
import funnelChart from "@/components/funnelChart/index.vue";
import radarChart from "@/components/radarChart/index.vue";
import roseChart from "@/components/roseChart/index.vue";
import columnChart from "@/components/columChart/index.vue";
import {
  monthlyIncomeData,
  incomeType,
  customDropData,
  customType,
  yearlyIncomeData,
  customJob,
  salesData,
  yearSalesData
} from "@/constants/mockData/dasthboard";

export default Vue.extend({
  data() {
    return {
      monthlyIncomeData: {},
      incomeType: {},
      lostData: {},
      customTypeData: {},
      yearlyIncomeData: {},
      customJobData: {},
      yearSalesData: {},
      salesData: {},
      lineOptions: {
        enableMarkLine: false
      },
      pieOptions: {
        legend: {
          show: true,
          position: "right",
          float: "center",
          fontColor: "#59595f",
          itemGap: 10,
          padding: 5,
          lineHeight: 26,
          margin: 5,
          borderWidth: 1
        }
      },
      funnelOptions: {
        legend: {
          show: true,
          fontColor: "#59595f",
          itemGap: 10,
          padding: 5,
          lineHeight: 26,
          margin: 5,
          borderWidth: 1
        }
      },
      radarOptions: {
        dataLabel: true,
        legend: {
          show: true,
          fontColor: "#59595f"
        },
        extra: {
          radar: { opacity: 0.4 }
        }
      },
      roseOptions: {
        legend: {
          fontColor: "#59595f"
        }
      },
      columnOptions: {
        legend: {
          fontColor: "#59595f"
        },
        yAxis: {
          max: 8000,
          min: 5000
        }
      },
      yAxis: {
        max: 70,
        min: 35,
        format: val => `￥${val}百万`
      }
    };
  },
  onLoad() {
    this.monthlyIncomeData = monthlyIncomeData;
    this.incomeType = incomeType;
    this.lostData = customDropData;
    this.customTypeData = customType;
    this.yearlyIncomeData = yearlyIncomeData;
    this.customJobData = customJob;
    this.salesData = salesData;
    this.yearSalesData = yearSalesData;
    this.yearColumnOptions = {
      ...this.columnOptions,
      dataLabel: false
    };
  },
  components: {
    "line-chart": lineChart,
    "donut-chart": pieChart,
    "funnel-chart": funnelChart,
    "radar-chart": radarChart,
    "rose-chart": roseChart,
    "column-chart": columnChart
  }
});
</script>
<style>
.body {
  overflow: hidden;
  padding: 0 12px;
  background-color: #23243b;
  min-height: 100vh;
}

.over-all {
  display: flex;
  justify-content: space-between;
  padding: 32px;
  color: white;
}

.income {
  padding: 0 12px;
  border-left: 2px solid #5a9eaf;
}

.stat {
  padding: 0 12px;
  border-left: 2px solid #354688;
}

.price {
  font-weight: bold;
  margin-bottom: 4px;
}

.catgory {
  font-size: 14px;
}
</style>