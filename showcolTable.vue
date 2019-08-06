<template>
	<div class="app-container">
	 <el-table :data="list" style="width: 100%">
     <el-table-column type="expand">
      <template slot-scope="props">
        <el-form label-position="left" inline class="demo-table-expand">
          <el-form-item label="商品名称">
            <span>{{ props.row.name }}</span>
          </el-form-item>
          <el-form-item label="所属店铺">
            <span>{{ props.row.shop }}</span>
          </el-form-item>
          <el-form-item label="商品 ID">
            <span>{{ props.row.id }}</span>
          </el-form-item>
          <el-form-item label="店铺 ID">
            <span>{{ props.row.shopId }}</span>
          </el-form-item>
          <el-form-item label="商品分类">
            <span>{{ props.row.category }}</span>
          </el-form-item>
          <el-form-item label="店铺地址">
            <span>{{ props.row.address }}</span>
          </el-form-item>
          <el-form-item label="商品描述">
            <span>{{ props.row.desc }}</span>
          </el-form-item>
        </el-form>
      </template>
    </el-table-column>
	<el-table-column type='index' :index="indexMethod" label="序号" width='80px'></el-table-column>
    <el-table-column label="商品 ID" prop="id"></el-table-column>
    <el-table-column label="商品名称" prop="name"></el-table-column>
    <el-table-column label="描述" prop="desc"></el-table-column>
  </el-table>
  <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
</div>
</template>

<script>
	import Pagination from '@/components/Pagination' 
	export default{
		name:'ShowColTable',
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
						shopId:'TR12345',
						name: "小六汤包" + key,
						shop:'小二家的店',
						date: '2019-03-21',
						category:'食物类',
						address: '陕西省榆林市榆阳区',
						email: '975676589@qq.com',
						desc:'百年老店'
					});
				}
			this.total = 100;
		},
	},
	}
</script>

<style>
	.demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
</style>
