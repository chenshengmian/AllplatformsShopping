<template>
	<view>
		<div class="gird-contails">
			<el-card class="box-card">
				<template #header>
					<div class="card-header">
						<span>电子钱包历史记录</span>
						<!-- <el-button class="button" text>Operation button</el-button> -->
					</div>
				</template>
				<div>
					<div class="mony">
						<div style="font-size: 30rpx;">钱包</div>
						<div>
							<el-select v-model="select" slot="prepend" placeholder="请选择" size="medium"
								style="width: 1820rpx">
								<el-option label="现金积分 (CP)" value="1"></el-option>
								<el-option label="旅游积分 (TP)" value="2"></el-option>
								<el-option label="Product Point (PP)" value="3"></el-option>
							</el-select>
						</div>
					</div>
					<div class="datamonth">
						<div style="font-size: 30rpx;">年-月</div>
						<div>
							<div class="block" style="display: inline-block;">
								<el-select v-model="mouth" slot="prepend" placeholder="请选择" size="medium"
									style="width: 900rpx;margin-right: 20rpx;">
									<div v-for="(item,index) in mouthArr">
										<el-option :label="item" :value="item"></el-option>
									</div>
								</el-select>
							</div>
							<div class="block" style="display: inline-block;">
								<el-select v-model="year" slot="prepend" placeholder="请选择" size="medium"
									style="width: 900rpx;">
									<div v-for="(item,index) in yearArr">
										<el-option :label="item" :value="item"></el-option>
									</div>
								</el-select>
							</div>
						</div>
					</div>
					<div class="sumbit" style="display: flex;justify-content: end;">
						<el-button type="primary" size="medium" @tap="handlechanginfo">提交</el-button>
					</div>
				</div>
				<el-table :data="tableData" class="custom-table">
					<el-table-column label="ID" width="40">
						<template slot-scope="scope">
							{{ (scope.$index+1)+(currentPage-1)*pageSize }}
						</template>
					</el-table-column>
					<el-table-column prop="timestr" label="日期" align="center">
					</el-table-column>
					<el-table-column prop="remark" label="交易说明" width="380" align="center">
					</el-table-column>
					<el-table-column prop="num" label="进账(-)为出账" align="center">
					</el-table-column>
					<el-table-column prop="credittype" label="类型" align="center">
						<template slot-scope="scope">
							<div v-if="scope.row.credittype=='credit1'">现金积分 (CP)</div>
							<div v-else-if="scope.row.credittype=='credit2'">旅游积分 (TP)</div>
							<div v-else>Product Point (PP)</div>
						</template>
					</el-table-column>
				</el-table>
				<div class="pagination" style="display: flex;justify-content: center;margin-top: 20rpx;">
					<el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange"
						:current-page="currentPage" :page-sizes="[10, 20, 30, 40]" :page-size="pageSize"
						layout="total, sizes, prev, pager, next" :total="counttotal"></el-pagination>
				</div>
			</el-card>
		</div>
	</view>
</template>

<script>
	export default {
		name: "wallet-records",
		data() {
			return {
				select: '',
				value2: '',
				value3: '',
				mouth: '',
				year: '',
				mouthArr: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September',
					'October', 'November', 'December'
				],
				yearArr: [],
				counttotal: 0,
				tableData: [], // 表格数据源
				currentPage: 1, // 当前页码
				pageSize: 10, // 每页显示的条数
			};
		},
		mounted() {
			this.getMounth()
			this.getuserinfo()
		},
		methods: {
			getMounth() {
				const current = new Date()
				const yearNew = current.getFullYear()
				this.yearArr = [yearNew - 5, yearNew - 4, yearNew - 3, yearNew - 2, yearNew - 1, yearNew]
				const mouthNew = current.getMonth()
				this.mouth = this.mouthArr[mouthNew]
				this.year = yearNew
			},
			handlechanginfo() {
				this.getuserinfo()
			},
			// 处理每页显示条数变化
			handleSizeChange(val) {
				// console.log('处理每页显示条数变化',this.pageSize)
				this.pageSize = val;
				this.getuserinfo();
			},
			// 处理当前页码变化
			handleCurrentChange(val) {
				// console.log('处理当前页码变化',val)
				this.currentPage = val;
				this.getuserinfo();
			},
			getuserinfo() {
				let _this = this
				let query = '&type=' + _this.select + '&page=' + _this.currentPage + '&pagesize=' + _this.pageSize +
					'&month=' + _this.mouth + '&year=' + _this.year
				_this.$axios.get('/plugin/index.php?i=1&f=guide&m=many_shop&d=mobile&r=uniapp.kyc.creditdetail' + query)
					.then(res => {
						console.log(res)
						const {
							result: {
								list,
								total
							}
						} = res
						_this.tableData = list
						_this.counttotal = Number(total)
					})
					.catch(err => {
						console.log(err)
					})
			}
		}
	}
</script>

<style>
	.gird-contails {
		display: grid;
		grid-template-columns: 100%;
	}

	.card-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.text {
		font-size: 14px;
	}

	.item {
		margin-bottom: 18px;
	}

	.el-input__suffix-inner {
		display: none !important;
	}

	.mony {
		display: flex;
		justify-content: space-between;
		margin-top: 10rpx;
	}

	.datamonth {
		display: flex;
		justify-content: space-between;
		margin-top: 10rpx;
	}

	.sumbit {
		/* margin-left: 840rpx; */
		margin-top: 10rpx;
	}

	.el-select {
		width: 100%;
	}

	/* 在屏幕宽度小于990px时 */
	@media screen and (max-width: 990px) {
		.el-select {
			margin-top: 20rpx;
			width: 600rpx !important;
		}

		.mony {
			display: grid;
			grid-template-columns: 1fr;
			margin-top: 10rpx;
		}

		.datamonth {
			display: grid;
			grid-template-columns: 1fr;
			margin-top: 10rpx;
		}

		.sumbit {
			margin-left: 0rpx;
			margin-top: 10rpx;
		}

		table {
			width: auto !important;
		}
	}
</style>