<template>
	<view class="out-box">
		<view class="inner-box">
			<view class="uni-list">
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						寻亲编码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="searchNum" placeholder="请输入" disabled />
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
			<view class="uni-list">
				<view class="uni-list-cell" v-for="(item,index) in formListTwo" :key="index">
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
				searchNum: '124355',
				existNum: 'hhhsad123242ddx',
				formList: [
					{
						name: '失踪人姓名',
						key: 'missName',
					},{
						name: '性别',
						key: 'missSex',
					},{
						name: '出生日期',
						key: 'missBirthday',
					},{
						name: '失踪日期',
						key: 'missDate',
					},{
						name: '失踪时的身高',
						key: 'missHeight',
					},{
						name: '是否采血',
						key: 'missTfBlood',
					},{
						name: '是否报案',
						key: 'missTfReport',
					},{
						name: '失踪人籍贯',
						key: 'missNative',
					},{
						name: '失踪地点',
						key: 'missPlace',
					},{
						name: '失踪详细地址',
						key: 'missPlaceDetail',
					},{
						name: '失踪人特征描述',
						key: 'missFeature',
					},{
						name: '失踪经过',
						key: 'missProcess',
					},{
						name: '家庭背景及线索',
						key: 'missBackground',
					},{
						name: '有无唤起孩子记忆',
						key: 'missTfMemory',
					},{
						name: '其他资料',
						key: 'missOtherData',
					},{
						name: '其他说明',
						key: 'missOtherExplain',
					}
				],
				formListTwo: [{
					name: '联系人姓名',
					key: 'contactName',
				},{
					name: '与失踪人关系',
					key: 'contactRelation',
				},{
					name: '手机号',
					key: 'contactPhone',
				},{
					name: '地址',
					key: 'contactAddress',
				},],
				form: {
					"missName": "可可",
					"missSex": "女",
					"missBirthday": "2020-04-26",
					"missDate": "2020-04-26",
					"missHeight": 160,
					"missTfBlood": "是",
					"missTfReport": "否",
					"missNative": "",
					"missPlace": "",
					"missPlaceDetail": "",
					"missFeature": "",
					"missProcess": "",
					"missBackground": "",
					"missTfMemory": "",
					"missOtherData": "",
					"missOtherExplain": "",
					"contactName": "小白",
					"contactRelation": "",
					"contactPhone": "",
					"contactAddress": ""
				},

			}
		},
		created() {
			this.formList = this.transformList(this.formList)
			this.formListTwo = this.transformList(this.formListTwo)
			// this.formList = this.formList.map((item) => {
			// 	for(let itemForm in this.form) {
			// 		if(itemForm == item.key) {
			// 			item.value = this.form[itemForm]
			// 		}
			// 	}
			// 	return {
			// 		...item
			// 	}
			// })
			// console.log('formList => ',this.formList)
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
					url: '/pages/registerPerson/index'
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
