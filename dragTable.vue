<template>
	<div class="app-container">
		 <el-table :data="list" border height="400" :summary-method="getSummaries"
    show-summary style="width: 100%; margin-top: 20px">
		<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
    <el-table-column prop="id" label="ID" width="180"></el-table-column>
    <el-table-column prop="name" label="姓名"></el-table-column>
    <el-table-column prop="amount1" label="数值 1（元）"></el-table-column>
    <el-table-column prop="amount2" label="数值 2（元）"></el-table-column>
    <el-table-column prop="amount3" label="数值 3（元）"></el-table-column>
  </el-table>
	<pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
	</div>
</template>
<script>
	import Pagination from '@/components/Pagination' 
	 export default{
		 name:'DragTable',
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
						id:'018798',
						name: "小六汤包" + key,
						amount1:'23',
						amount2: '23.5',
						amount3: 12
					});
				}
			this.total = 100;
		},
		getSummaries(param) {
        const { columns, data } = param;
        const sums = [];
        columns.forEach((column, index) => {
          if (index === 0) {
            sums[index] = '总价';
            return;
          }
          const values = data.map(item => Number(item[column.property]));
          if (!values.every(value => isNaN(value))) {
            sums[index] = values.reduce((prev, curr) => {
              const value = Number(curr);
              if (!isNaN(value)) {
                return prev + curr;
              } else {
                return prev;
              }
            }, 0);
            sums[index] += ' 元';
          } else {
            sums[index] = 'N/A';
          }
        });

        return sums;
      }
	 },
	 }
</script>
<style>
	
</style>