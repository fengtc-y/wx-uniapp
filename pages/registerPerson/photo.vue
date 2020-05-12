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
			<view class="uni-padding-wrap uni-common-mt">
				<view class="demo">
					<block v-if="imageSrc">
						<image :src="imageSrc" class="image" mode="widthFix"></image>
					</block>
					<block v-else>
						<view class="uni-hello-addfile" @click="chooseImage">+ 选择图片</view>
					</block>
				</view>
			</view>
			<button type="primary" @click="confirm">完成</button>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				searchNum: '124355',
				existNum: 'hhhsad123242ddx',
				imageSrc: '',
			}
		},
		methods: {
			chooseImage: function() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					sourceType: ['album'],
					success: (res) => {
						console.log('chooseImage success, temp path is', res.tempFilePaths[0])
						var imageSrc = res.tempFilePaths[0]
						uni.uploadFile({
							// url: 'https://unidemo.dcloud.net.cn/upload',
							url: '',
							filePath: imageSrc,
							fileType: 'image',
							name: 'data',
							success: (res) => {
								console.log('uploadImage success, res is:', res)
								uni.showToast({
									title: '上传成功',
									icon: 'success',
									duration: 1000
								})
								this.imageSrc = imageSrc
							},
							fail: (err) => {
								console.log('uploadImage fail', err);
								uni.showModal({
									content: err.errMsg,
									showCancel: false
								});
							}
						});
					},
					fail: (err) => {
						console.log('chooseImage fail', err)
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = res.authSetting['scope.album'];
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			confirm() {
				uni.navigateTo({
				    url: '/pages/registerPerson/detail'
				})
			}
		}
	}
</script>

<style scoped>
	.uni-list-cell-left {
		width: 180upx;
	}
	.uni-list-cell-db {
		color: #A4A4A4;
	}
	.image {
		width: 100%;
	}
	.demo {
		background: #FFF;
		padding: 50upx;
	}
	.uni-hello-addfile {
	    text-align: center;
	    line-height: 300upx;
	    background: #FFF;
	    padding: 50upx;
	    margin-top: 10px;
	    font-size: 38upx;
	    color: #808080;
	}
	.uni-padding-wrap{
		width:100%;
		margin-bottom: 30upx;
		padding: 0;
	}
</style>
