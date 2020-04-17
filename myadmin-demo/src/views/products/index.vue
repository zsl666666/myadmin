<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
    >
      <el-table-column align="center" label="序号" width="95">
        <template slot-scope="scope">
          {{ scope.$index+1 }}
        </template>
      </el-table-column>
      <el-table-column label="商品ID" width="95">
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="商品名称" width="120">
        <template slot-scope="scope">
          {{ scope.row.name }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="商品价格" width="120">
        <template slot-scope="scope">
          {{ scope.row.price }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="实际价格" width="120">
        <template slot-scope="scope">
          {{ scope.row.salePrice }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="商品卖点" width="120">
        <template slot-scope="scope">
          {{ scope.row.salePoint }}
        </template>
      </el-table-column>
      <el-table-column label="操作" align="center" width="230" class-name="small-pading fixed-width">
        <template slot-scope="scope">
          <el-button type="primary" size="mini" @click="editpro(scope.row.id)">
            编辑
          </el-button>
          <el-button type="danger" size="mini" @click="deletepro(scope.row.id)">
            删除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { getList } from '@/api/table'
import { getProductsdata,deleteIddata } from '@/network/products'


export default {
  data() {
    return {
      list: null,
      listLoading: true
    }
  },
  created() {
    // this.fetchData()
    this.getProductsdata()
  },
  methods: {
    // fetchData() {
    //   this.listLoading = true
    //   getList().then(response => {
    //     this.list = response.data.items
    //     this.listLoading = false
    //   })
    // }
    editpro(id){
      this.$router.push("/editproduct/index/"+id)
    },
    deletepro(id){
      // console.log(id)
      deleteIddata(id).then( res=>{
        console.log('删除成功')
        this.getProductsdata()
      })
    },
    getProductsdata(){
      this.listLoading = true
      getProductsdata().then(res => {
        // console.log(res)
        this.list = res.data
        this.listLoading = false
      })
    }
  }
}
</script>
