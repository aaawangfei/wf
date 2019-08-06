<template>
	<div class="app-container">
	 <el-row class='table-filter'>
		 <el-col>
			 <el-button size='mini' type="primary" class='btn-delete' @click="multDelete">批量删除</el-button>
		 </el-col>
	 </el-row> 	
	 <el-table :data="list" stripe style="width: 100%" ref="multipleTable" @selection-change="handleSelectionChange" height="400">
	<el-table-column type="selection" width="55"></el-table-column>
	<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
	<el-table-column prop="name" label="姓名"></el-table-column>
	<el-table-column prop="date" label="日期"></el-table-column>
	<el-table-column prop="address" label="地址" :show-overflow-tooltip="true"></el-table-column>
	<el-table-column prop="email" label="邮箱" :show-overflow-tooltip="true"></el-table-column>
	<el-table-column fixed="right" label="操作" width='150'>
		<template slot-scope="scope" >
		<el-button type="text" size="small">查看</el-button>
		<el-button type="text" size="small">编辑</el-button>
		<el-button type="text" size="small" @click="dialogVisible = true">删除</el-button>
	   </template>
	</el-table-column>
  </el-table>
	<pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
	<el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
  <span>确定删除吗？（删除后不可恢复）</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
 </el-dialog>
</div>
</template>

<script>
	import Pagination from '@/components/Pagination' 
	export default {
	    name: 'CheckboxTable',
		components: { Pagination },
        data(){
		 return{
		  list: null,
          total: 0,
          listLoading: true,
		  multipleSelection: [],
		  dialogVisible: false,
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
				});
			}
		this.total = 100;
     },
	  handleSelectionChange(val) {
        this.multipleSelection = val;
		// console.log(this.multipleSelection);
      },
	  multDelete(){
		 if(this.multipleSelection.length == 0){
			 this.$message.error('请选择要删除的数据');
		 }  
		 else{
			this.dialogVisible=true;
		 }
	  }
	}
	}
</script>

<style>
	.table-filter{
		margin: 10px 0 20px;
	}
	.btn-delete{
		float: right;
	}
</style>
