<template>
	<div class="app-container">
	 <el-table :data="tableData" stripe style="width: 100%" :default-sort = "{prop: 'post_id', order: 'descending'}">
	<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
	<el-table-column prop="post_id"sortable label="id"></el-table-column>
	<el-table-column prop="title" sortable :show-overflow-tooltip="true" label="标题"></el-table-column>
    <el-table-column prop="created_at"sortable sortable label="发表时间"></el-table-column>    
	<el-table-column prop="author_name" label="作者"></el-table-column>
  </el-table>
	<pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" /> 
	</div>
</template>
<script>
	import Pagination from '@/components/Pagination' 
	export default {
	    name: 'SortTable',
		components: { Pagination },
        data(){
		 return{
		  tableData:[],	 
		  list: null,
          total: 0,
          listLoading: true,
          listQuery: {
            page: 1,
            limit: 20,
         },
	  }
	 },
	 
     created(){     
         this.getList();   
       },
	methods:{
		indexMethod(index) {
             return index + 1;
         },    
	    formatter(row, column) {
        return row.address;
        },
	    getList(){
			 var _this = this   //很重要！！
			this.$axios('https://unidemo.dcloud.net.cn/api/news')
			    .then(function (res) {
			        console.log(res);
			        _this.tableData = res.data
					_this.total = res.data.length;
			    })
			    .catch(function (error) {
			        console.log(error);
			    });
		}
//          getList(){
// 			 var _this = this ;
// 			 this.$axios = ('https://unidemo.dcloud.net.cn/api/news')
// 			 .then(function(res){
// 				 _this.tableData = res.data
// 				 for(var i = 0; i < this.listQuery.limit; i++) {
// 				 	var key = (this.listQuery.page - 1) * this.listQuery.limit + i;
// 				 	this.tableData.push({
// 				 		_this.post_id = res.data.post_id
// 				 	});
// 				 }
// 				_this.total = res.data.length;
// 			 })
// 			 .catch(function(err){
// 				  console.log(error);
// 			 })
// 			 		
// 		 }
           
		
	}
	}
</script>

<style>
	
</style>
