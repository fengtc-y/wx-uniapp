<template>
	<view>
			<view class="text-box" scroll-y="true">
				<text class="title">{{title}}</text>
				<text class="explain">{{explain}}</text>
				<text class="explain" v-for="(item,index) in contentList" :key="index">{{item}}</text>
				<button type="primary" size="mini" @click="iAgree">我同意</button>
			</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: "志愿者说明",
				  explain:
					"是由关爱儿童的各界爱心人士自愿组成的民间志愿者组织进行寻亲登记之前，请认真阅读以下内容及法律声明：当您的孩子失踪或被拐后，请马上拨打110报警。",
				  contentList: [
					"1、宝贝回家寻子网接受失踪或被拐时16周岁以下儿童的登记信息及流浪乞讨儿童的登记信息，超过16周岁或不属于失踪或被拐的儿童信息，需在家属同意并且相关资料完整的情况下在“其他寻人”区域进行登记。如果您所登记的信息超过16周岁资料信息不完整或不属于失踪被拐范围，请访问宝贝回家论坛的其它寻人版块http://bbs.baobeihuijia.com/forum-21-1.html，注册后将寻亲信息发布在其它寻人版块。",
					"2、本协会为寻亲者提供免费的寻人帮助，请如实填写您在网站登记的资料。",
					"3、请不要利用宝贝回家寻子网站发布虚假寻人信息或恶作剧信息，本协会将保留一切追究法律责任的权利。",
					"4、以下情况，请您与您的家人或孩子现在的抚养人协商后再决定是否进行登记操作：①离家出走；②被亲生父亲或母亲带走；③将亲生子女卖掉或送人；④父母离异，孩子判给另一方，想要回孩子的抚养权。",
					"5、由于网络的连通性及实时性的特殊，您在宝贝回家登记的信息通过审核后，将会被转载到全国各地的论坛，宝贝回家只能对本站及论坛的资料进行修改及删除，无法对被转载到其它论坛的资料进行修改及删除等操作。"
				  ]
			}
		},
		methods: {
			iAgree() {
				uni.navigateTo({
				    url: '/pages/volunteer/register'
				})
			}
		}
	}
</script>

<style scoped>
	.text-box {
		/* margin-bottom: 60upx; */
		padding: 20upx 0 30upx 0;
		display: flex;
		min-height: 300upx;
		background-color: #FFFFFF;
		justify-content: center;
		flex-direction: column;
		font-size: 30upx;
		color: #353535;
		line-height: 1.8;
	}
	.title {
		font-size: 36upx;
		font-weight: 700;
		text-align: center;
	}
	.explain {
		text-indent: 56upx;
		padding: 0 10upx;
	}
</style>
