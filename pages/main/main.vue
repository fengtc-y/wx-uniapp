<template>
	<view class="content">
		<view v-if="hasLogin" class="hello">
			<view class="title">
				您好 {{userName}}，您已成功登录。
			</view>
			<!-- <view class="ul">
				<view>这是 uni-app 带登录模板的示例App首页。</view>
				<view>在 “我的” 中点击 “退出” 可以 “注销当前账户”</view>
			</view> -->
		</view>
		<view v-if="!hasLogin" class="hello">
			<view class="title">
				您好 游客。
			</view>
			<!-- <view class="ul">
				<view>这是 uni-app 带登录模板的示例App首页。</view>
				<view>在 “我的” 中点击 “登录” 可以 “登录您的账户”</view>
			</view> -->
			<view class="chart-area">
				<view class="chart-item" ref="chart-item" id="chart-item"></view>
				<view class="chart-data">
					<view class="data-item">
						<text class="text-item item-top" style="color:#FF0000">{{`${missForm.missed.total}人`}}</text>
						<text class="text-item item-mid">累计失踪</text>
						<text class="text-item">上月
							<text style="color:#FF0000;font-weight: 700;">{{`+${missForm.missed.bfMonth}`}}</text>
							人</text>
					</view>
					<view class="data-item">
						<text class="text-item item-top" style="color:#04B431">{{`${missForm.found.total}人`}}</text>
						<text class="text-item item-mid">累计找回</text>
						<text class="text-item">上月
							<text style="color:#04B431;font-weight: 700;">{{`-${missForm.found.bfMonth}`}}</text>
							人</text>
					</view>
				</view>

			</view>
		</view>
	</view>
</template>

<script>
	import {
		mapState
	} from 'vuex'
	import echarts from 'echarts'
	import chinaJson from 'echarts/map/json/china.json'

	export default {
		computed: mapState(['forcedLogin', 'hasLogin', 'userName']),
		data() {
			return {
				missForm: {
					missed: {
						total: 1004,
						bfMonth: 55
					},
					found: {
						total: 400,
						bfMonth: 17
					}
				},
				today: new Date(),
			}
		},
		onLoad() {
			if (!this.hasLogin) {
				uni.showModal({
					title: '未登录',
					content: '您未登录，需要登录后才能继续',
					/**
					 * 如果需要强制登录，不显示取消按钮
					 */
					showCancel: !this.forcedLogin,
					success: (res) => {
						if (res.confirm) {
							/**
							 * 如果需要强制登录，使用reLaunch方式
							 */
							if (this.forcedLogin) {
								uni.reLaunch({
									url: '../login/login'
								});
							} else {
								uni.navigateTo({
									url: '../login/login'
								});
							}
						}
					}
				});
			}
		},
		mounted() {
			this.drawLine();
		},
		methods: {
			drawLine() {
				let chart = document.getElementById('chart-item');
				if (chart) {
					echarts.registerMap('China', chinaJson);
					let myChart = echarts.init(chart);
					myChart.setOption({
						title: {
							text: '全国失踪人口实时地图',
							subtext: `数据来源于MissPerson Beta, 统计截至${this.today.getFullYear()}年${this.today.getMonth()+1}月${this.today.getDate()-1}日24时`,
							top: 5,
							left: 5
						},
						visualMap: {
							type: 'piecewise',
							left: 'right',
							min: 0,
							splitNumber: 5,
							pieces: [{
									gt: 500,
									label: '500人以上'
								}, // 不指定 max，表示 max 为无限大（Infinity）。
								{
									gt: 300,
									lte: 500,
									label: '300-500人'
								},
								{
									gt: 100,
									lte: 300,
									label: '100-300人'
								},
								{
									gt: 10,
									lte: 100,
									label: '10-100人'
								},
								{
									lt: 10,
									label: '10人以下'
								} // 不指定 min，表示 min 为无限大（-Infinity）。
							],
							// color: ['#e0f3f8', '#abd9e9', '#74add1', '#4575b4', '#313695'],
							color: ['#d94e5d', '#eac736', '#50a3ba'],
							textStyle: {
								color: '#000'
							}
						},
						tooltip: {
							trigger: 'item'
						},
						series: [{
							type: 'map',
							roam: true,
							map: 'China',
							emphasis: {
								label: {
									show: true
								}
							},
							data: [{
									name: '安徽',
									value: 299
								},
								{
									name: '河北',
									value: 12
								},
								{
									name: '江苏',
									value: 57
								},
								{
									name: '河南',
									value: 490
								}, {
									name: '四川',
									value: 890
								},
							]
						}]
					});
				}
			}
		}
	}
</script>

<style>
	.hello {
		display: flex;
		flex: 1;
		flex-direction: column;
	}

	.title {
		color: #8f8f94;
		margin-top: 50upx;
	}

	.ul {
		font-size: 30upx;
		color: #8f8f94;
		margin-top: 50upx;
	}

	.ul>view {
		line-height: 50upx;
	}

	.chart-area {
		background-color: #fff;
		margin: 20upx 0;
		height: 900upx;
	}

	.chart-item {
		height: 700upx;
	}

	.chart-data {
		display: flex;
		justify-content: center;
		height: 200upx;
	}

	.data-item {
		width: 200upx;
	}

	.text-item {
		display: block;
		text-align: center;
	}

	.item-top {
		font-size: 40upx;
		font-weight: 700;
	}

	.item-mid {
		color: #848484;
	}
</style>
