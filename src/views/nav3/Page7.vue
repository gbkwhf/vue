<template>
	<div class="block">
		<span class="demonstration">默认</span>
		<el-date-picker v-model="value1" type="date" placeholder="选择日期"></el-date-picker>
		<!--switch开关-->
		<el-switch style="display: block;padding: 10px 0 10px 0;" active-text="按月付费" inactive-text="按年付费" v-model="value3"></el-switch>
		<el-switch style="display:block" v-model="value2" active-color="#13ce66" inactive-color="#ff4949" active-text="按月付费" inactive-text="按年付费"></el-switch>
		<!------表格------->
		<el-table :data="tableData" stripe height="200" style="width: 80%" :default-sort="{prop: 'date', order: 'descending'}">
			<el-table-column prop="date" fixed label="日期" width="180" sortable></el-table-column>
			<el-table-column prop="name" label="姓名" width="180" sortable></el-table-column>
			<el-table-column prop="address" label="地址"></el-table-column>
			<el-table-column label="操作" width="150">
				<template scope="scope">
					<el-button size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
					<el-button type="danger" size="small" @click="handleDel(scope.$index, scope.row)">删除</el-button>
				</template>
			</el-table-column>
		</el-table>
		<!----------线性进度条---->
		<el-progress :text-inside="true" :stroke-width="18" :percentage="70" style="margin: 10px;"></el-progress>
		<!------环形进度条------->
		<el-progress type="circle" :percentage="30"></el-progress>
		<!--------轮播图-------->
		<span class="demonstration">轮播图</span>
		<el-carousel trigger="click" height="150px">
			<el-carousel-item v-for="item in 4" :key="item">
				<h3>{{ item }}</h3>
			</el-carousel-item>
		</el-carousel>
		<!----------计数器---------->
		<el-input-number v-model="num1" @change="handleChange" :min="1" :max="10" label="描述文字" style="margin-top: 10px;"></el-input-number>
		<div>
			<p>{{num2}}</p>
			<p @click="numClick">查看数字</p>
			<p>{{num3}}</p>
			<p @click="_comClick">查看数字</p>
			<p @click="changeNum">改变数值+10</p>
		</div>
		<!------switch滑块------------>
		<!--<div class="block">
	    <el-slider
	      v-model="value8"
	      show-input>
	    </el-slider>
  		</div>-->
	</div>
	
</template>
<style type="text/css">
	.el-carousel__item:nth-child(2n) {
     background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
     background-color: #d3dce6;
  }
</style>
<script>
import util from '../../common/js/util'
	//import NProgress from 'nprogress'
	import { getUserListPage, removeUser, batchRemoveUser, editUser, addUser } from '../../api/api';
	let no={'num':30};
	export default {
	
		data() {
			return {
				value1: '',
				value3: '',
				value2: '',
				num1:1,
				t:no,
				num2:no.num,
				//				value8:9
				'tableData': [{
					date: '2016-05-02',
					name: '李小虎',
					address: '上海市普陀区金沙江路 1518 弄',
				}, {
					date: '2016-05-04',
					name: '王小虎',
					address: '上海市普陀区金沙江路 1517 弄'
				}, {
					date: '2016-05-01',
					name: '王小虎',
					address: '上海市普陀区金沙江路 1519 弄'
				}, {
					date: '2016-05-03',
					name: '王小虎',
					address: '上海市普陀区金沙江路 1516 弄'
				}]
			};
		},
		computed:{
			num3(){
				return no.num
			}
		},
		methods:{
			handleChange(value) {
        		console.log(value);
      		},
      		numClick(){
  				console.log("这是data里的值:",this.num2);
      		},
      		_comClick(){
      			console.log("这是computed里的值:",this.num3);
      		},
      		changeNum(){
      			no.num+=10;
      			console.log(no.num)
      		},
      		//获取用户列表
			getUsers() {
				let para = {
					page: this.page,
					name: this.filters.name
				};
				this.listLoading = true;
				//NProgress.start();
				getUserListPage(para).then((res) => {
					this.total = res.data.total;
					this.users = res.data.users;
					this.listLoading = false;
					//NProgress.done();
				});
			},
			//删除
      		handleDel: function (index, row) {
				this.$confirm('确认删除该记录吗?', '提示', {
					type: 'warning'
				}).then(() => {
					this.listLoading = true;
					//NProgress.start();
					let para = { id: row.id };
					removeUser(para).then((res) => {
						this.listLoading = false;
						//NProgress.done();
						this.$message({
							message: '删除成功',
							type: 'success'
						});
						this.getUsers();
					});
				}).catch(() => {

				});
			},
		}
	};
</script>