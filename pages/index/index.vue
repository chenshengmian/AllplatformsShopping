<template>
	<view class="content">
		<div style="display: flex;justify-content: center;width: 100%;background-color: #F5F5F5;">
			<div class="homepage">
				<website-homepage @getstatus="getstatus" />
			</div>
		</div>
		<div class="footers">Copyright 2023. Felement Sdn Bhd. All Right Reserved.</div>
	</view>
</template>

<script>
	import WebsiteHomepage from '@/components/website-homepage/website-homepage.vue'
	export default {
		components: {
			WebsiteHomepage,
		},
		data() {
			return {

			}
		},
		mounted() {
			
		},
		methods: {
			
		}
	}
</script>

<style scoped>
	.footers {
		height: 120rpx;
		line-height: 120rpx;
		width: 100%;
		font-size: 26rpx;
		background-color: #fff;
		color: rgb(91, 98, 107);
		text-align: center;
	}
	
	@media screen and (max-width: 990px) {
		.homepage {
			width: 100% !important;
		}

	}

	.homepage {
		width: 80%;
	}

	


	/* 设置滚动条的轨道样式 */
	::-webkit-scrollbar {
		width: 8px;
		/* 滚动条宽度 */
	}

	/* 设置滚动条的滑块样式 */
	::-webkit-scrollbar-thumb {
		background-color: #409EFF;
		/* 滑块背景颜色 */
		border-radius: 4px;
		/* 滑块圆角 */
	}

	/* 设置滚动条的滑道样式 */
	::-webkit-scrollbar-track {
		background-color: #f1f1f1;
		/* 滑道背景颜色 */
		border-radius: 4px;
		/* 滑道圆角 */
	}
</style>