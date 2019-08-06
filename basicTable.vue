<template>
	<div class="app-container">
	 <el-table :data="list" stripe style="width: 100%">
		<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
		<el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="date" label="日期"></el-table-column>
    <el-table-column prop="address" label="地址"></el-table-column>
		<el-table-column prop="email" label="邮箱"></el-table-column>
  </el-table>
	<pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
	</div>
</template>

<script>
	import Pagination from '@/components/Pagination' 
	export default {
	    name: 'BasicTable',
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
					address: '陕西省榆林市榆阳区',
					email: '975676589@qq.com',
				});
			}
		this.total = 100;
    },
	}
	}
</script>

<style>
	
</style>
