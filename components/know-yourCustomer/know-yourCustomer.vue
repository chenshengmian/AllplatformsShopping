<template>
	<view>
		<el-card>
			<el-form :model="ruleForm"  :label-position="labelPosition"  :rules="rules" ref="ruleForm" label-width="200px" class="demo-ruleForm">
				<el-form-item label="Identity card (Front) 身份证前" prop="idcard_pre">
					<el-input v-model="ruleForm.idcard_pre"></el-input>
				</el-form-item>
				<el-form-item label="Account Holder 持卡者名字" prop="account_holder">
					<el-input v-model="ruleForm.account_holder"></el-input>
				</el-form-item>
				<el-form-item label="Account Holder 持卡者名字" prop="account_holder">
					<el-input v-model="ruleForm.account_holder"></el-input>
				</el-form-item>
				<el-form-item label="Bank Name 银行名字" prop="bank_name">
					<el-switch v-model="ruleForm.bank_name"></el-switch>
				</el-form-item>
				<el-form-item label="Bank Branch 银行分行" prop="bank_branch">
					<el-switch v-model="ruleForm.bank_branch"></el-switch>
				</el-form-item>
				<el-form-item label="Bank Account Number 户口号码" prop="bank_account_number">
					<el-switch v-model="ruleForm.bank_account_number"></el-switch>
				</el-form-item>
				<el-form-item label="活动形式" prop="desc">
					<el-input type="textarea" v-model="ruleForm.desc"></el-input>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
					<el-button @click="resetForm('ruleForm')">重置</el-button>
				</el-form-item>
			</el-form>
		</el-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				labelPosition:'right',
				ruleForm: {
					name: '',
					region: '',
					date1: '',
					date2: '',
					delivery: false,
					type: [],
					resource: '',
					desc: ''
				},
				rules: {
					name: [{
							required: true,
							message: '请输入活动名称',
							trigger: 'blur'
						},
						{
							min: 3,
							max: 5,
							message: '长度在 3 到 5 个字符',
							trigger: 'blur'
						}
					],
					region: [{
						required: true,
						message: '请选择活动区域',
						trigger: 'change'
					}],
					date1: [{
						type: 'date',
						required: true,
						message: '请选择日期',
						trigger: 'change'
					}],
					date2: [{
						type: 'date',
						required: true,
						message: '请选择时间',
						trigger: 'change'
					}],
					type: [{
						type: 'array',
						required: true,
						message: '请至少选择一个活动性质',
						trigger: 'change'
					}],
					resource: [{
						required: true,
						message: '请选择活动资源',
						trigger: 'change'
					}],
					desc: [{
						required: true,
						message: '请填写活动形式',
						trigger: 'blur'
					}]
				}
			};
		},
		mounted() {
			this.getScreenWidth(); // 初始化获取屏幕宽度和缩放比例
			window.addEventListener('resize', this.handleResize); // 监听窗口大小变化
		},
		beforeDestroy() {
			window.removeEventListener('resize', this.handleResize); // 移除监听事件
		},
		methods: {
			getScreenWidth() {
				this.screenWidth = window.innerWidth;
				if (this.screenWidth <= 990) {
					// this.labelw = '220rpx'
					this.labelPosition = 'top'
				} else {
					this.labelPosition = 'right'
				}
			},
			handleResize() {
				const newScreenWidth = window.innerWidth;
				if (newScreenWidth !== this.screenWidth) {
					this.screenWidth = newScreenWidth;
					console.log(newScreenWidth);
					if (newScreenWidth <= 990) {
						this.labelPosition = 'top'
					} else {
						this.labelPosition = 'right'
					}
				}
			},
			submitForm(formName) {
				this.$refs[formName].validate((valid) => {
					if (valid) {
						alert('submit!');
					} else {
						console.log('error submit!!');
						return false;
					}
				});
			},
			resetForm(formName) {
				this.$refs[formName].resetFields();
			}
		}
	}
</script>

<style>
	.el-card {
		font-size: 26rpx;
	}

	.title {
		text-align: center;
		font-size: 26rpx;
		color: #5B626B;
	}
</style>