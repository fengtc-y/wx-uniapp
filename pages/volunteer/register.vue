<template>
	<view class="out-box">
		<view class="inner-box">
			<form @submit="formSubmit" @reset="formReset">
				<page-head :title="title"></page-head>
				<view class="form-item">
					<view class="title">用户名</view>
					<input class="uni-input" name="userName" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">密码</view>
					<input class="uni-input" password name="userPassword" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">姓名</view>
					<input class="uni-input" name="realName" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">性别</view>
					<radio-group name="userSex">
						<label>
							<radio value="男" /><text>男</text>
						</label>
						<label>
							<radio value="女" /><text>女</text>
						</label>
					</radio-group>
				</view>
				<view class="form-item">
					<view class="title">年龄</view>
					<input class="uni-input" type="number" name="userAge" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">身份证号</view>
					<input class="uni-input" type="idcard" name="userCard" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">手机号</view>
					<input class="uni-input" type="number" name="userPhone" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">常驻地</view>
					<input class="uni-input" name="userPlace" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">详细地址</view>
					<input class="uni-input" name="userPlaceDetail" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">职业</view>
					<input class="uni-input" name="userJob" placeholder="请输入" />
				</view>
				<view class="form-item">
					<view class="title">其他联系方式</view>
					<input class="uni-input" name="userContact" placeholder="请输入" />
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
				title: '志愿者个人信息',
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
				    url: '/pages/volunteer/photo'
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
