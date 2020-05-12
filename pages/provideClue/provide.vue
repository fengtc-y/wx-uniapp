<template>
	<view class="out-box">
		<view class="inner-box">
			<view class="uni-list">
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						志愿者编码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="volunteerNum" placeholder="请输入志愿者编码查询" />
					</view>
					<image class="image" mode="widthFix" @click="searchUser" src="../../static/img/search.png" />
				</view>
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						失踪人员编码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="missNum" placeholder="请输入" disabled />
					</view>
				</view>
			</view>
			
			<view v-show="userTrue">
				<page-head :title="titleOne"></page-head>
				<view class="uni-list">
					<view class="uni-list-cell" v-for="(item,index) in listUser" :key="index">
						<view class="uni-list-cell-left">
							{{item.name}}
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" :value="item.value" disabled />
						</view>
					</view>
				</view>
				<page-head :title="titleTwo"></page-head>
				<view class="uni-list">
					<view class="uni-list-cell" v-for="(item,index) in listMiss" :key="index">
						<view class="uni-list-cell-left">
							{{item.name}}
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" :value="item.value" disabled />
						</view>
					</view>
				</view>
				<page-head :title="titleThree"></page-head>
				<view class="uni-list">
					<view class="uni-list-cell" v-for="(item,index) in listClue" :key="index">
						<view class="uni-list-cell-left">
							{{item.name}}
						</view>
						<view class="uni-list-cell-db">
							<input class="uni-input" :value="item.value" disabled />
						</view>
					</view>
				</view>
			</view>
			<button type="primary" @click="nextStep">下一步</button>
		</view>
		
		<!-- 确认密码 弹框 -->
		<uni-popup ref="showtip" type="center" :mask-click="false">
			<view class="uni-tip">
				<!-- <text class="uni-tip-content">这是一个通过自定义 popup，自由扩展的 警告弹窗。点击遮罩不会关闭弹窗。</text> -->
				<view class="uni-list-cell">
					<view class="uni-list-cell-left">
						密码
					</view>
					<view class="uni-list-cell-db">
						<input class="uni-input" :value="userPassword" @input="inputPwd" password placeholder="请输入密码" />
					</view>
				</view>
				<view class="uni-tip-group-button">
					<text class="uni-tip-button" @click="cancel">取消</text>
					<text class="uni-tip-button" @click="confirm">确定</text>
				</view>
			</view>
		</uni-popup>
		<message ref="Message"></message>

	</view>
</template>

<script>
	import pageHead from '@/components/page-head.vue'
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	import message from '@/components/bobo-message/bobo-message.vue'
	export default {
		components:{
			pageHead,
			uniPopup,
			message,
		},
		data() {
			const {formUser,formMiss,formClue} = {
				formUser: {
					"realName": "志愿者1",
					"userCard": "",
					"userPhone": "",
					"userPlaceDetail": "",
				},
				formMiss: {
					"missName": "流浪1",
					"missSex": "",
					"missBirthday": "",
					"missDate": "",
					"missPlace": "",
					"contactName": "",
					"contactRelation": "",
					"contactPhone": "",
				},
				formClue: {
					"clueDate": "",
					"missPlace": "江苏无锡",
					"missPlaceDetail": "",
					"missProcess": "",
					'missOtherExplain': "",
				},
			}
			return {
				volunteerNum: '',
				missNum: '',
				listUser: [{
						name: '姓名',
						key: 'realName',
					},{
						name: '身份证号',
						key: 'userCard',
					},{
						name: '手机号',
						key: 'userPhone',
					},{
						name: '详细地址',
						key: 'userPlaceDetail',
					}
				],
				listMiss: [{
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
						name: '失踪地点',
						key: 'missPlace',
					},{
						name: '联系人姓名',
						key: 'contactName',
					},{
						name: '与失踪人关系',
						key: 'contactRelation',
					},{
						name: '手机号',
						key: 'contactPhone',
					}
				],
				listClue: [{
						name: '线索日期',
						key: 'clueDate',
					},{
						name: '线索省市',
						key: 'missPlace',
					},{
						name: '详细地址',
						key: 'missPlaceDetail',
					},{
						name: '失踪经过',
						key: 'missProcess',
					},{
						name: '其他说明',
						key: 'missOtherExplain',
					}
				],
				formUser: formUser,
				formMiss: formMiss,
				formClue: formClue,
				titleOne: '志愿者信息',
				titleTwo: '失踪人员信息',
				titleThree: '线索信息',
				userTrue: false,
				userPassword: '',
			}
		},
		created() {
			this.listUser = this.tfUser(this.listUser)
			this.listMiss = this.tfMiss(this.listMiss)
			this.listClue = this.tfClue(this.listClue)
		},
		mounted() {
		},
		methods: {
			searchUser() {
				this.$refs['showtip'].open()
			},
			inputPwd(event) {
				this.userPassword = event.target.value
			},
			confirm() {
				if(this.userPassword == '123') {
					this.$refs['showtip'].close()
					this.userTrue = true
				}else {
					this.$refs['Message'].error('密码错误 , 请重新输入')
				}
				
			},
			cancel() {
				this.$refs['showtip'].close()
			},
			nextStep() {
				uni.navigateTo({
					url: '/pages/provideClue/selectClue'
				})
			},
			tfUser(list) {
				return list.map((item) => {
					for(let itemForm in this.formUser) {
						if(itemForm == item.key) {
							item.value = this.formUser[itemForm]
						}
					}
					return {
						...item
					}
				})
			},
			tfMiss(list) {
				return list.map((item) => {
					for(let itemForm in this.formMiss) {
						if(itemForm == item.key) {
							item.value = this.formMiss[itemForm]
						}
					}
					return {
						...item
					}
				})
			},
			tfClue(list) {
				return list.map((item) => {
					for(let itemForm in this.formClue) {
						if(itemForm == item.key) {
							item.value = this.formClue[itemForm]
						}
					}
					return {
						...item
					}
				})
			},
		}
	}
</script>

<style scoped>
	.uni-list {
		margin-bottom: 30upx;
	}

	.uni-list-cell-left {
		width: 180upx;
	}

	.uni-list-cell-db {
		color: #A4A4A4;
	}

	.image {
		/* margin: 20upx 0; */
		width: 80upx;
	}

	.uni-center {
		margin-bottom: 30upx;
	}
	
	/* 提示窗口 */
		.uni-tip {
			/* #ifndef APP-NVUE */
			display: flex;
			flex-direction: column;
			/* #endif */
			padding: 15px;
			width: 300px;
			background-color: #fff;
			border-radius: 10px;
		}
	
		.uni-tip-content {
			/* padding: 15px;
	*/
			font-size: 14px;
			color: #666;
		}
	
		.uni-tip-group-button {
			/* #ifndef APP-NVUE */
			display: flex;
			/* #endif */
			flex-direction: row;
			margin-top: 20px;
		}
		.uni-tip-button {
			flex: 1;
			text-align: center;
			font-size: 14px;
			color: #3b4144;
		}
		.uni-tip .uni-list-cell-left {
			width: 90upx;
		}
		.uni-tip .uni-input {
			background-color: #D8D8D8;
		}
		.uni-tip .uni-input-placeholder {
			color: #000;
		}
</style>
