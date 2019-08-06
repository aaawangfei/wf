<template>
  <div>
    <div class="app-container">
      <tree-table ref="TreeTable" :data="tableData" :default-expand-all="true" 
	  :columns="columns" border default-children="children">
        <template slot="pre-column">
          <el-table-column type="expand" width="55">
            <template>
              <el-tag type="info">
                这里只是一个占位符插槽，您可以显示任何东西。
              </el-tag>
            </template>
          </el-table-column>
        </template>
        <template slot="append" slot-scope="{scope}">
         <el-button size="mini" type="primary" @click="addMenuItem(scope.row,'brother')">增加兄弟</el-button>
         <el-button size="mini" type="primary" @click="addMenuItem(scope.row,'children')">增加孩子</el-button>
        </template>
        <template slot="operation" slot-scope="{scope}">
          <el-button size="mini" type="success" @click="editItem(scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="deleteItem(scope.row)">删除</el-button>
        </template>
      </tree-table>
    </div>
	<!-- 编辑弹出框 -->
    <el-dialog :visible.sync="dialogFormVisible" title="编辑">
      <el-form :model="tempItem" label-width="100px" style="width:600px">
        <el-form-item label="名字">
          <el-input v-model.trim="tempItem.name" placeholder="Name"/>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取消</el-button>
        <el-button type="primary" @click="updateItem">确认</el-button>
      </span>
    </el-dialog>
	<!-- 删除弹出框 -->
	<el-dialog :visible.sync="dialogDeleteVisible" title="提示">
	   <span>确定删除吗？（删除后不可恢复）</span>  
	   <span slot="footer" class="dialog-footer">
	    <el-button @click="dialogDeleteVisible = false">取消</el-button>
	    <el-button type="primary" @click="removeItem">删除</el-button>
	  </span>
	</el-dialog>
  </div>
</template>
<script>
import TreeTable from '@/components/TreeTable'
import data from './data.js'

export default {
  components: { TreeTable },
  data() {
    return {
      tableData: [],
      tempItem: {},
      dialogFormVisible: false,
	  dialogDeleteVisible:false,
      columns: [
        {
          label: '名字',
          key: 'name',
          expand: true
        },
       
        {
          label: '节点',
          key: 'append',
          width: 300
        },
        {
          label: '操作',
          key: 'operation',
          width: 160
        }
      ],
	  rowNum:{
		  
	  }
    }
  },
  created() {
    this.getData()
  },
  methods: {
    getData() {
      this.tableData = data
    },
    editItem(row) {
      this.tempItem = Object.assign({}, row)
      this.dialogFormVisible = true
    },
    async updateItem() {
      await this.$refs.TreeTable.updateTreeNode(this.tempItem)
      this.dialogFormVisible = false
    },
    addMenuItem(row, type) {
      if (type === 'children') {
        this.$refs.TreeTable.addChild(row, { name: 'child'})
      }

      if (type === 'brother') {
        this.$refs.TreeTable.addBrother(row, { name: 'brother' })
      }
    },
	deleteItem(row) {
	  this.rowNum = row;
	  this.dialogDeleteVisible = true
	  
	},
	removeItem(){
		this.$refs.TreeTable.delete(this.rowNum);
		this.dialogDeleteVisible = false
	}
  }
}
</script>
