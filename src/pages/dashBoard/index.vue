<template>
  <view class="body dark-theme">
    <view class="over-all">
      <view class="income">
        <view class="price">￥155（百万）</view>
        <view class="catgory">总收入</view>
      </view>
      <view class="stat">
        <view class="price">700（千）</view>
        <view class="catgory">乘次</view>
      </view>
    </view>
    <view class="chart-container">
      <line-chart
        id="monthlyIncome"
        header="年度收入趋势"
        v-bind:initData="monthlyIncomeData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:yAxis="yAxis"
        v-bind:options="lineOptions"
      ></line-chart>
    </view>
    <view class="chart-container">
      <donut-chart
        id="incomeType"
        header="收入类型占比"
        v-bind:initData="incomeType"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="pieOptions"
      ></donut-chart>
    </view>
    <view class="chart-container">
      <funnel-chart
        id="funnelType"
        header="用户丢失率分析"
        v-bind:initData="lostData"
        v-bind:width="700"
        v-bind:height="500"
        v-bind:options="funnelOptions"
      ></funnel-chart>
    </view>
    <view class="chart-container">
      <radar-chart
        id="radarType"
        header="用户类型分析"
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

const monthlyIncomeData = {
  categories: ["1月", "2月", "3月", "4月", "5月", "6月"],
  series: [
    {
      name: "收入",
      data: [59, 53, 50, 45, 60, 55]
    }
  ]
};

const incomeType = {
  series: [
    {
      name: "机票",
      data: 42
    },
    {
      name: "餐饮",
      data: 20
    },
    {
      name: "座位",
      data: 25
    },
    {
      name: "娱乐",
      data: 10
    },
    {
      name: "其他",
      data: 3
    }
  ]
};

const customDropData = {
  series: [
    {
      name: "首页",
      data: 100
    },
    {
      name: "购票",
      data: 89
    },
    {
      name: "选择座位",
      data: 67
    },
    {
      name: "选择食物",
      data: 50
    },
    {
      name: "支付",
      data: 45
    }
  ]
};

const customType = {
  categories: ["男", "女", "儿童", "青年", "中年", "老年"],
  series: [
    {
      name: "4月",
      data: [49, 51, 10, 35, 38, 17]
    },
    {
      name: "5月",
      data: [52, 48, 16, 38, 35, 11]
    },
    {
      name: "6月",
      data: [40, 60, 12, 30, 43, 15]
    }
  ]
};

export default Vue.extend({
  data() {
    return {
      monthlyIncomeData: {},
      incomeType: {},
      lostData: {},
      customTypeData: {},
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
  },
  components: {
    "line-chart": lineChart,
    "donut-chart": pieChart,
    "funnel-chart": funnelChart,
    "radar-chart": radarChart
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