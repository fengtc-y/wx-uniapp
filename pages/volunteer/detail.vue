<template>
	<view class="out-box">
		<view class="inner-box">
			<view class="uni-list">
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						志愿者编码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="volunteerNum" placeholder="请输入" disabled />
					</view>
				</view>
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						唯一存证编码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="existNum" placeholder="请输入" disabled />
					</view>
				</view>
			</view>
			<view class="uni-center" style="background:#FFFFFF; font-size:0;">
				<image class="image" mode="widthFix" src="../../static/img/noPhoto.png" />
				<image class="image" mode="widthFix" src="../../static/img/noPhoto.png" />
				<image class="image" mode="widthFix" src="../../static/img/noPhoto.png" />
			</view>
			<view class="uni-list">
				<view class="uni-list-cell" v-for="(item,index) in formList" :key="index">
					<view class="uni-list-cell-left">
						{{item.name}}
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="item.value" disabled />
					</view>
				</view>
			</view>

			<button type="primary" @click="backHome">返回主页</button>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				volunteerNum: 'LS110',
				existNum: 'hhhsad123242ddx',
				formList: [
					{
						name: '用户名',
						key: 'userName',
					},{
						name: '姓名',
						key: 'realName',
					},{
						name: '性别',
						key: 'userSex',
					},{
						name: '年龄',
						key: 'userAge',
					},{
						name: '身份证号',
						key: 'userCard',
					},{
						name: '手机号',
						key: 'userPhone',
					},{
						name: '常驻地',
						key: 'userPlace',
					},{
						name: '详细地址',
						key: 'userPlaceDetail',
					},{
						name: '职业',
						key: 'userJob',
					},{
						name: '其他联系方式',
						key: 'userContact',
					}
				],
				form: {
					"userName": "Jike",
					"userPassword": "123",
					"realName": "季客",
					"userSex": "男",
					"userAge": 40,
					"userCard": "",
					"userPhone": "",
					"userPlace": "",
					"userPlaceDetail": "",
					"userJob": "",
					"userContact": "",
				},

			}
		},
		created() {
			this.formList = this.transformList(this.formList)
		},
		mounted() {
		},
		methods: {
			transformList(list) {
				return list.map((item) => {
					for(let itemForm in this.form) {
						if(itemForm == item.key) {
							item.value = this.form[itemForm]
						}
					}
					return {
						...item
					}
				})
			},
			backHome() {
				uni.switchTab({
					url: '/pages/volunteer/index'
				})
			}
		}
	}
</script>

<style scoped>
	.uni-list {
		margin-bottom: 30upx;
	}

	.uni-list-cell-left {
		width: 240upx;
	}

	.uni-list-cell-db {
		color: #A4A4A4;
	}

	.image {
		margin: 20upx 0;
		width: 200upx;
	}

	.uni-center {
		margin-bottom: 30upx;
	}
</style>
