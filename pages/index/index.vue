<template>
	<view class="content">
		<div style="display: flex;justify-content: center;width: 100%;background-color: #F5F5F5;">
			<div class="homepage">
				<website-homepage @getstatus="getstatus" />
			</div>
		</div>
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
		mounted(param) {
			// console.log(1111)
			this.login()
			// console.log(uni.getStorageSync('tokenArray'))
			this.getScreenWidth(); // 初始化获取屏幕宽度和缩放比例
			window.addEventListener('resize', this.handleResize); // 监听窗口大小变化
		},
		beforeDestroy() {
			window.removeEventListener('resize', this.handleResize); // 移除监听事件
		},
		methods: {
			 handleCustomButton() {
			    // 执行自定义按钮的操作
				const content = document.getElementById("print");
				console.log(content)
				window.print(content)
			},
			
			async login() {

			},
		
			getdatail(res) {
				// const lastarr = res[res.length -1]
				// // console.log(lastarr)
				const {
					id,
					index
				} = res
				this.todatail = res
				this.index = index
			},
			getIndex(data) {
				// console.log(data)
				const {
					index,
					nodeid
				} = data
				this.index = index
				this.nodeid = nodeid
			},

	
			changeStatus() {
				let self = this
				self.isCollapse = !self.isCollapse
				self.disable = !self.disable
				self.classp = !self.classp
			},
			showDrawer() {
				// console.log(111)
				this.drawerVisible = !this.drawerVisible;
			},
			toggleFullscreen() {
				const element = document.documentElement; // 获取整个文档的根元素
				// console.log(element)
				if (element.requestFullscreen) {
					// 兼容不同浏览器的API调用方式
					element.requestFullscreen();
				} else if (element.mozRequestFullScreen) { // Firefox
					element.mozRequestFullScreen();
				} else if (element.webkitRequestFullscreen) { // Chrome, Safari和Opera
					element.webkitRequestFullscreen();
				} else if (element.msRequestFullscreen) { // IE/Edge
					element.msRequestFullscreen();
				}
			},
			showDrawerleft() {
				this.drawerVisibletwo = !this.drawerVisibletwo;
				// this.isblock = true
			},
			handleDrawerClose() {
				this.isblock = false
			},
			getScreenWidth() {
				this.screenWidth = window.innerWidth;
				if (this.screenWidth <= 990) {
					this.drawerSize = '60%'
					this.width = '90%'
				} else {
					this.drawerSize = '15%'
				}
			},
			handleResize() {
				const newScreenWidth = window.innerWidth;
				if (newScreenWidth !== this.screenWidth) {
					this.screenWidth = newScreenWidth;
					console.log(newScreenWidth);
					if (newScreenWidth <= 990) {
						this.drawerSize = '60%'
						this.width = '90%'
					} else {
						this.drawerSize = '15%'
					}
				}
			},
			handleOptionChange(option) {
				if (option === 'option1') {
					this.option2 = !this.option1; // 关闭选项2并开启选项1
				} else if (option === 'option2') {
					this.option1 = !this.option2; // 关闭选项1并开启选项2
				}
				this.option1 == true ? (this.baColr = '#F2F2F2', this.hColr = '#fff', this.footbg = '#FAFAFA', this
					.topColor = '#fff', this.drawbg = '#fff') : (this.baColr = '#1F2431', this.hColr = '#7A6FBE', this
					.footbg = '#323A4E',
					this.topColor = '#7A6FBE', this.drawbg = '#2A3142')
			},
			handleSelect(index) {
				// console.log(index);
				let self = this
				self.index = index
				this.drawerVisible = false
			},
		}
	}
</script>

<style>

	

	.setting {
		margin-left: 20rpx;
		display: inline-block;
		animation: rotation 2s infinite linear;
	}

	.drawerright {
		font-weight: 1000;
	}

	@keyframes rotation {
		from {
			transform: rotate(0deg);
		}

		to {
			transform: rotate(360deg);
		}
	}

	.el-menu-vertical-demo:not(.el-menu--collapse) {
		width: 400rpx;
		min-height: 800rpx;
	}

	.userLogo {
		margin-left: 10rpx;
		padding: 30rpx;
		width: 100rpx;
		height: 100rpx;
	}

	.userLo {
		padding: 22rpx;
		width: 90%;
		height: 80rpx;
		margin-left: 20rpx;
		margin-top: 18rpx;
	}

	.el-switch {
		margin-left: 25rpx;
	}

	.el-row span {
		display: inline-block;
		margin-top: 20rpx;
		margin-left: 20rpx;
	}

	.changeStatu,
	.changeStatuw {
		font-size: 45rpx;
		margin-top: 30rpx;
		cursor: pointer;
	}

	@media screen and (max-width: 1400px) {
		.userLo {
			width: 70%;
		}
	}

	@media screen and (max-width: 990px) {
		.el-header {
			height: 120rpx !important;
			/* position: fixed; */
			/* top:0; */
		}

		.homepage {
			width: 100% !important;
		}

		.changeStatu {
			display: none;
		}

		.changeStatuw {
			display: block !important;
		}

		.asos,
		.fullsc,
		.placeholder {
			display: none;
		}

		.changeStatus1 {
			display: block !important;
			font-size: 50rpx;
			margin-top: 30rpx;
			cursor: pointer;
			width: 100%;
		}

		.smalllogo {
			width: 55rpx;
			height: 55rpx;
		}

		.atvatr {
			width: 84%;
			left: 0rpx;
		}

		.ableta {
			position: fixed;
			width: 400rpx;
			top: 100rpx;
			margin-top: 20rpx;
			z-index: 99;
		}

		.newplaceholder {
			width: 0rpx;
			height: 100vh;
			visibility: hidden;
			/* 或者使用 opacity: 0; */
		}

		.footer {
			font-size: 20rpx;
		}
	}

	.homepage {
		width: 80%;
		height: 100vh;
	}

	.changeStatus1,
	.changeStatuw {
		display: none;
	}

	.el-main {
		height: 86vh;
		/* position: absolute; */
		top: 100rpx;
		z-index: 1;
		/* width: 100%; */
	}

	.el-menu {
		position: fixed;
		/* right: 400rpx; */
	}


	.headerTop {
		display: flex;
		/* z-index: 9999; */
		/* width: 100%; */
		position: fixed;
		background-color: #fff;
	}

	.el-header {
		height: 120rpx;
	}

	.footer {
		line-height: 120rpx;
		text-align: center;
		font-size: 26rpx;
		color: rgb(91, 98, 107);
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