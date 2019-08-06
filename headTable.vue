<template>
	<div class="app-container">
		<el-table :data="list" stripe style="width: 100%;" height="400" >
				<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
			<el-table-column prop="name" label="姓名" ></el-table-column>
		  <el-table-column prop="date" label="日期" ></el-table-column>
      <el-table-column prop="address" label="地址" :show-overflow-tooltip="true"></el-table-column>	 
			<el-table-column prop="email" label="邮箱" :show-overflow-tooltip="true"></el-table-column>
			<el-table-column prop="telephone" label="电话"></el-table-column>
			<el-table-column fixed="right" label="操作" width='150'>
        <template slot-scope="scope" >
        <el-button type="text" size="small">查看</el-button>
        <el-button type="text" size="small">编辑</el-button>
				<el-button type="text" size="small">删除</el-button>
       </template>
    </el-table-column>
		</el-table>
		<pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
		
	</div>
</template>

<script>
	import Pagination from '@/components/Pagination'
	export default{
		name:'HeadTable',
		components: { Pagination },
		data(){
				 return{
				 list: null,
		     total: 0,
		     listLoading: true,
		     listQuery: {
		       page: 1,
		       limit: 20,
		       title: undefined,
		       type: undefined,
		    },
		 }
		},
		 created(){
		  this.getList()
		 },
		methods:{
			indexMethod(index) {
		    return index + 1;
		  },
			getList() {
			     this.list = [];
					 for(var i = 0; i < this.listQuery.limit; i++) {
						var key = (this.listQuery.page - 1) * this.listQuery.limit + i;
						this.list.push({
							name: "小六汤包" + key,
							date: '2019-03-21',
							address: '陕西省榆林市榆阳区陕西省榆林市榆阳区',
							email: '975676589@qq.com',
							telephone:'18149120606',
							name1:'111111',
							name2:'000000',
						});
					}
				this.total = 100;
			},
			
		}
	}
</script>

<style>
	.el-table__body{
    table-layout:auto !important;
}
</style>
