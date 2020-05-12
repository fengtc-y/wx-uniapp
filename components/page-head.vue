<template name="page-head">
	<view class="uni-page-head">
		<view class="uni-page-head-title">{{title}}</view>
	</view>
</template>
<script>
	export default {
		name: "page-head",
		props: {
			title: {
				type: String,
				default: ""
			}
		}
	}
</script>
<style scoped>
	.uni-page-head-title {
		color: #007AFF;
		border-bottom: 1px solid #007AFF;
	}
</style>
