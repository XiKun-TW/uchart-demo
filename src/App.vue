<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  mpType: "app",
  onLaunch() {
    console.log("App Launch");
  },
  onShow() {
    console.log("App Show");
  },
  onHide() {
    console.log("App Hide");
  }
});
</script>

<style>
body {
  background-color: #e4e4e4;
}
/*每个页面公共css */
.chart-container {
  background-color: #ffffff;
  padding: 0 12px;
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
  box-shadow: 1px 2px 8px rgba(0, 0, 0, 0.2);
}

.chart-header {
  font-size: 16px;
  color: #007aff;
  margin: 12px 0;
  padding-left: 4px;
  border-left: 4px solid #007aff;
}
/*每个页面公共css */

.dark-theme .chart-container {
  background-color: #2b2d48;
}

.dark-theme .chart-header {
  color: #5e617b;
  border: none;
}
</style>
