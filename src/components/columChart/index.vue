<template>
	<view>
		<view v-if="header" class="chart-header">{{header}}</view>
		<view class="chart-canvas">
			<canvas v-bind:canvas-id="id" v-bind:id="id" v-bind:style="style" class="charts" @touchstart="touchColumn"></canvas>
		</view>
	</view>
</template>

<script>
	import uCharts from '@/uCharts/u-charts.js';
	var _self;

	export default {
		data() {
			return {
				cWidth:'',
				cHeight:'',
				pixelRatio:1,
				style: {},
				canvas: null
			}
		},
		props: {
			initData: Object,
			width: Number,
			height: Number,
			header: String,
			rotate: false,
			id: String
		},
		mounted() {
			_self = this;

			const { initData, width, height, id } = _self.$props;
			
			this.style = {
				width: `${(width - 40) *_self.pixelRatio}upx`,
				height: `${height *_self.pixelRatio}upx`
			}
			this.cWidth=uni.upx2px(width - 40);
			this.cHeight=uni.upx2px(height);
			
			if(initData) {
				_self.showColumn(id,initData);
			}
		},
		methods: {
			showColumn(canvasId,chartData){
				const {rotate} = _self.$props;
				_self.canvas = new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'column',
					legend:{show:true},
					fontSize:11,
					background:'#FFFFFF',
					pixelRatio:_self.pixelRatio,
					animation: true,
					rotate: !!rotate,
					categories: chartData.categories,
					series: chartData.series,
					xAxis: {
						disableGrid:true,
					},
					yAxis: {
						//disabled:true
					},
					dataLabel: true,
					width: _self.cWidth*_self.pixelRatio,
					height: _self.cHeight*_self.pixelRatio,
					extra: {
						column: {
							type:'group',
							width: _self.cWidth*_self.pixelRatio*0.45/chartData.categories.length,
						}
					  }
				});
				
			},
			touchColumn(e){
				_self.canvas.showToolTip(e, {
					format: function (item, category) {
						if(typeof item.data === 'object'){
							return category + ' ' + item.name + ':' + item.data.value 
						}else{
							return category + ' ' + item.name + ':' + item.data 
						}
					}
				});
			},
		}
	}
</script>
<style>
</style>
