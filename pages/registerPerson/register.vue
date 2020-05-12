<template>
	<view class="out-box">
		<view class="inner-box">
			<form @submit="formSubmit" @reset="formReset">
				<page-head :title="titleOne"></page-head>
				<view class="form-item">
					<view class="title">失踪人姓名</view>
					<input class="uni-input" name="missName" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">性别</view>
					<radio-group name="missSex">
						<label>
							<radio value="男" /><text>男</text>
						</label>
						<label>
							<radio value="女" /><text>女</text>
						</label>
					</radio-group>
				</view>
				<view class="form-item">
					<view class="title">出生日期</view>
					<view class="uni-list-cell-db">
						<picker name="missBirthday" mode="date" :value="missBirthday" :start="startDate" :end="endDate" @change="bindBirthday">
							<view class="uni-input">{{missBirthday}}</view>
						</picker>
					</view>
				</view>
				<view class="form-item">
					<view class="title">失踪日期</view>
					<view class="uni-list-cell-db">
						<picker name="missDate" mode="date" :value="missDate" :start="startDate" :end="endDate" @change="bindMissDate">
							<view class="uni-input">{{missDate}}</view>
						</picker>
					</view>
				</view>
				<view class="form-item">
					<view class="title">失踪时的身高</view>
					<uni-number-box name="missHeight" :value="missHeight" @change="bindMissHeight" :max="250"></uni-number-box>
				</view>
				<view class="form-item">
					<view class="title">是否采血</view>
					<radio-group name="missTfBlood">
						<label>
							<radio value="是" /><text>是</text>
						</label>
						<label>
							<radio value="否" /><text>否</text>
						</label>
					</radio-group>
				</view>
				<view class="form-item">
					<view class="title">是否报案</view>
					<radio-group name="missTfReport">
						<label>
							<radio value="是" /><text>是</text>
						</label>
						<label>
							<radio value="否" /><text>否</text>
						</label>
					</radio-group>
				</view>
				<view class="form-item">
					<view class="title">失踪人籍贯</view>
					<input class="uni-input" name="missNative" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">失踪地点</view>
					<input class="uni-input" name="missPlace" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">失踪详细地址</view>
					<input class="uni-input" name="missPlaceDetail" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">失踪人特征描述</view>
					<!-- <input class="uni-input" name="missFeature" placeholder="请输入" /> -->
					<textarea class="uni-textarea" name="missFeature" placeholder="请输入"/>
				</view>
				<view class="form-item">
					<view class="title">失踪经过</view>
					<textarea class="uni-textarea" name="missProcess" placeholder="请输入"/>
				</view>
				<view class="form-item">
					<view class="title">家庭背景及线索资料</view>
					<textarea class="uni-textarea" name="missBackground" placeholder="请输入"/>
				</view>
				<view class="form-item">
					<view class="title">有无唤起孩子记忆信息</view>
					<radio-group name="missTfMemory">
						<label>
							<radio value="是" /><text>是</text>
						</label>
						<label>
							<radio value="否" /><text>否</text>
						</label>
					</radio-group>
				</view>
				<view class="form-item">
					<view class="title">其他资料</view>
					<textarea class="uni-textarea" name="missOtherData" placeholder="请输入"/>
				</view>
				<view class="form-item">
					<view class="title">其他说明</view>
					<textarea class="uni-textarea" name="missOtherExplain" placeholder="请输入"/>
				</view>
				
				<page-head :title="titleTwo"></page-head>
				<view class="form-item">
					<view class="title">联系人姓名</view>
					<input class="uni-input" name="contactName" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">联系人与失踪人关系</view>
					<input class="uni-input" name="contactRelation" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">手机号</view>
					<input class="uni-input" name="contactPhone" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">地址</view>
					<input class="uni-input" name="contactAddress" placeholder="请输入" />
				</view>
				

				<view class="uni-btn-v">
					<button class="submitBtn" form-type="submit">下一步</button>
					<button type="default" form-type="reset">重新填写</button>
				</view>
			</form>
		</view>

	</view>
</template>

<script>
	import pageHead from '@/components/page-head.vue'
	import uniNumberBox from '@/components/uni-number-box/uni-number-box.vue'
	
	export default {
		components: {
			pageHead,
			uniNumberBox,
		},
		data() {
			const currentDate = this.getDate({
				format: true
			})
			return {
				titleOne: '失踪人信息',
				titleTwo: '联系人信息',
				missBirthday: currentDate,
				missDate: currentDate,
				missHeight: 0,
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		methods: {
			// 提交表单
			formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
				// var formdata = e.detail.value
				// uni.showModal({
				// 	content: '表单数据内容：' + JSON.stringify(formdata),
				// 	showCancel: false
				// });
				uni.navigateTo({
				    url: '/pages/registerPerson/photo'
				})
			},
			// 重置表单
			formReset: function(e) {
				console.log('清空数据')
			},
			// 出生日期绑定
			bindBirthday(e) {
				this.missBirthday = e.target.value
			},
			// 失踪日期绑定
			bindMissDate(e) {
				this.missDate = e.target.value
			},
			// 失踪身高绑定
			bindMissHeight(e) {
				this.missHeight = e
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 100;
				} else if (type === 'end') {
					year = year;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			}
		}
	}
</script>

<style scoped>
	.form-item .title {
		padding: 20upx 0;
	}
	.submitBtn {
		background-color: #007AFF;
		color: #fff;
	}
</style>
