<template>
	<view class="out-box">
		<view class="inner-box">
			<form @submit="formSubmit">
				<view class="uni-list">
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							失踪人姓名
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" name="missName" placeholder="请输入失踪人姓名" />
						</view>
					</view>
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							失踪人编码
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" name="missNum" placeholder="请输入失踪人编码" />
						</view>
					</view>
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							失踪地点
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" name="missPlace" placeholder="请输入失踪地点" />
						</view>
					</view>
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							联系人姓名
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" name="contactName" placeholder="请输入联系人姓名" />
						</view>
					</view>
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">
							联系人手机
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" name="contactPhone" placeholder="请输入联系人手机" />
						</view>
					</view>
				</view>
				<view class="uni-btn-v">
					<button class="submitBtn" type="primary" form-type="submit">查询</button>
				</view>
			</form>
			<view class="uni-list">
				<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(value, key) in listData" :key="key" @click="goDetail(value)">
					<view class="uni-media-list">
						<image class="uni-media-list-logo" :src="value.cover"></image>
						<view class="uni-media-list-body">
							<view class="uni-media-list-text-top">
								<text>{{ value.missName }}</text>
								<text>{{ value.missAge }}</text>
								<text>{{ value.missSex }}</text>
							</view>
							<view class="uni-media-list-text-bottom">
								<text>{{ value.missPlace }}</text>
								<text>{{ value.missDate }}</text>
							</view>
							<view class="uni-media-list-text-bottom">
								<text>{{ `存证编号：${value.missNum}` }}</text>
							</view>
						</view>
					</view>
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	import uniCard from '@/components/uni-card/uni-card.vue'
	export default {
		components:{
			uniCard
		},
		data() {
			return {
				listData: [
					{
						missName: "失踪者1",
						missAge: "35岁",
						missSex: '男',
						missPlace: "湖北省武汉市",
						missDate: '2018-01-29',
						missNum: '466XASKDJAUJ866QER',
						cover: "https://img.36krcdn.com/20200410/v2_9c3331af67e64994aa97a27fffb1a380_img_png?x-oss-process=image/resize,m_mfit,w_520,h_300/crop,w_520,h_300,g_center",
						id: 121375,
					},
					{
						missName: "失踪者扎扎奇亚1",
						missAge: "21岁",
						missSex: '女',
						missPlace: "内蒙古自治区呼和浩特市",
						missDate: '2018-01-29',
						missNum: '466XASKDJAUJ866QER',
						cover: "https://img.36krcdn.com/20200411/v2_16417a06088947debe0450950f8fc813_img_png",
						id: 121374,
					}
				]
			}	
		},
		methods: {
			formSubmit(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
			},
		}
	}
</script>

<style>
	.uni-list-cell-left {
		width: 180upx;
	}

.uni-media-list-logo {
	width: 180upx;
	height: 140upx;
}

.uni-media-list-body {
	height: auto;
	justify-content: space-around;
}

.uni-media-list-text-top {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	height: 56upx;
	font-size: 28upx;
	overflow: hidden;
}

.uni-media-list-text-bottom {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}
</style>
