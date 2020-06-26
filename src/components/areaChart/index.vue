<template>
	<view>
		<view v-if="header" class="chart-header">{{ header }}</view>
		<view class="chart-canvas" >
			<canvas v-bind:canvas-id="id" v-bind:id="id" v-bind:style="style" class="charts" @touchstart="touchArea"></canvas>
		</view>
	</view>
</template>

<script>
	import uCharts from '@/uCharts/u-charts.js';
	var _self;
	var canvaArea=null;
   
	export default {
		data() {
			return {
				cWidth:'',
				cHeight:'',
				pixelRatio:1,
				style: {}
			}
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
				width: `${(width - 40) *_self.pixelRatio}upx`,
				height: `${height *_self.pixelRatio}upx`
			}
			this.cWidth=uni.upx2px(width - 40);
			this.cHeight=uni.upx2px(height);
			
			if(initData) {
				_self.showArea(id,initData);
			}
		},
		methods: {
			showArea(canvasId,chartData){
				canvaArea=new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'area',
					fontSize:11,
					legend:true,
					dataLabel:false,
					dataPointShape:true,
					pixelRatio:_self.pixelRatio,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					xAxis: {
						type:'grid',
						gridColor:'#CCCCCC',
						gridType:'dash',
						dashLength:8
					},
					yAxis: {
						gridType:'dash',
						gridColor:'#CCCCCC',
						dashLength:8,
						splitNumber:5,
					},
					width: _self.cWidth*_self.pixelRatio,
					height: _self.cHeight*_self.pixelRatio,
					extra: {
						area:{
							type: 'straight',
							opacity:0.2,
							addLine:true,
							width:2
						}
					}
				});
				
			},
			touchArea(e) {
				canvaArea.showToolTip(e, {
					format: function (item, category) {
						return category + ' ' + item.name + ':' + item.data 
					}
				});
			}
		}
	}
</script>

<style>
</style>
