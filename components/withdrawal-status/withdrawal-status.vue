<template>
	<view>
		<div class="gird-contails">
			<el-card class="box-card">
				<template #header>
					<div class="card-header">
						<span>电子钱包取款状况</span>
						<!-- <el-button class="button" text>Operation button</el-button> -->
					</div>
				</template>
				<div class="yearmonth">
					<div style="display: flex;">
						<div class="month">
							<el-select v-model="mouth" slot="prepend" placeholder="请选择" size="medium" >
								<div v-for="(item,index) in mouthArr">
									<el-option :label="item" :value="item"></el-option>
								</div>
							</el-select>
						</div>
						<div class="year">
							<el-select v-model="year" slot="prepend" placeholder="请选择" size="medium" >
								<div v-for="(item,index) in yearArr">
									<el-option :label="item" :value="item"></el-option>
								</div>
							</el-select>
						</div>
					</div>
					<div class="sumbit">
						<el-button type="primary" size="medium" @tap="handlechanginfo">提款状况查询</el-button>
					</div>
				</div>
				 <el-table
				    :data="tableData"
					class="custom-table"
				   >
				   <el-table-column label="ID" width="40">
				   	<template slot-scope="scope">
				   		{{ (scope.$index+1)+(currentPage-1)*pageSize }}
				   	</template>
				   </el-table-column>
				   <el-table-column
				     prop="title"
				     label="标题"
					 align="center" 
				     >
				   </el-table-column>
				    <el-table-column
				      prop="timestr"
				      label="申请日期"
					  align="center" 
				      s>
				    </el-table-column>
				    <el-table-column
				      prop="logmes.bank_name"
					  align="center" 
				      label="银行名称">
				    </el-table-column>
					<el-table-column
					  prop="realname"
					  label="银行户口持有者"
					  align="center" 
					  >
					</el-table-column>
					<el-table-column
					  prop="logmes.bank_account_number"
					  align="center" 
					  label="银行账户号码">
					</el-table-column>
					<el-table-column
					  prop="money"
					  align="center" 
					  label="转账金额">
					</el-table-column>
					<el-table-column
					  prop="statusstr"
					  align="center" 
					  label="状况">
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
		name: "withdrawal-status",
		data() {
			return {
				mouth:'',
				year:'',
				mouthArr:['January','February','March','April','May','June','July','August','September','October','November','December'],
				yearArr:[],
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
		methods:{
			getMounth(){
				const current = new Date()
				const yearNew = current.getFullYear()
				this.yearArr = [yearNew-5,yearNew-4,yearNew-3,yearNew-2,yearNew-1,yearNew]
				const mouthNew = current.getMonth()
				this.mouth = this.mouthArr[mouthNew]
				this.year = yearNew
			},
			handlechanginfo(){
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
			getuserinfo(){
				let _this = this
				let query = '&type='+_this.select+'&page='+_this.currentPage+'&pagesize='+_this.pageSize+'&month='+_this.mouth+'&year='+_this.year
				_this.$axios.get('/plugin/index.php?i=1&f=guide&m=many_shop&d=mobile&r=uniapp.kyc.memberlog'+query)
					.then(res=>{
						console.log(res)
						const { result:{list,total} } = res
						_this.tableData = list
						_this.counttotal = Number(total)
					})
					.catch(err=>{
						console.log(err)
					})
			}
		}
	}
</script>

<style>
	.month,.year{
		margin-right: 20rpx;
	}
	.yearmonth {
		display: flex;
	}
	
	@media screen and (max-width: 990px) {
		.yearmonth {
			display: block !important;
		}
		.sumbit{
			margin-top: 20rpx;
		}
	}
</style>

