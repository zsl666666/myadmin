<template>
  <div class="app-container">
    <el-form ref="form" :model="product" label-width="120px">
      <el-form-item label="商品名称">
        <el-input v-model="product.name" />
      </el-form-item>
      <el-form-item label="商品价格">
        <el-input v-model="product.price" />
      </el-form-item>
      <el-form-item label="实际价格">
        <el-input v-model="product.salePrice" />
      </el-form-item>
      <el-form-item label="商品卖点">
        <el-input v-model="product.salePoint" />
      </el-form-item>
      
      <el-form-item>
        <el-button type="submit" @click="updatedata">编辑</el-button>
        <!-- <el-button @click="onCancel">Cancel</el-button> -->
      </el-form-item>
      <!-- <div>{{product}}</div> -->
      <!-- <el-form-item label="Activity name">
        <el-input v-model="form.name" />
      </el-form-item>
      <el-form-item label="Activity zone">
        <el-select v-model="form.region" placeholder="please select your zone">
          <el-option label="Zone one" value="shanghai" />
          <el-option label="Zone two" value="beijing" />
        </el-select>
      </el-form-item>
      <el-form-item label="Activity time">
        <el-col :span="11">
          <el-date-picker v-model="form.date1" type="date" placeholder="Pick a date" style="width: 100%;" />
        </el-col>
        <el-col :span="2" class="line">-</el-col>
        <el-col :span="11">
          <el-time-picker v-model="form.date2" type="fixed-time" placeholder="Pick a time" style="width: 100%;" />
        </el-col>
      </el-form-item>
      <el-form-item label="Instant delivery">
        <el-switch v-model="form.delivery" />
      </el-form-item>
      <el-form-item label="Activity type">
        <el-checkbox-group v-model="form.type">
          <el-checkbox label="Online activities" name="type" />
          <el-checkbox label="Promotion activities" name="type" />
          <el-checkbox label="Offline activities" name="type" />
          <el-checkbox label="Simple brand exposure" name="type" />
        </el-checkbox-group>
      </el-form-item>
      <el-form-item label="Resources">
        <el-radio-group v-model="form.resource">
          <el-radio label="Sponsor" />
          <el-radio label="Venue" />
        </el-radio-group>
      </el-form-item>
      <el-form-item label="Activity form">
        <el-input v-model="form.desc" type="textarea" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">Create</el-button>
        <el-button @click="onCancel">Cancel</el-button>
      </el-form-item> -->
    </el-form>
  </div>
</template>

<script>
import { getIddata } from '@/network/products'
import axios from 'axios'
export default {
  data() {
    return {
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      product: {}
    }
  },
  methods: {
    onSubmit() {
      
    },
    updatedata(){
      let newdata = {
          name: this.product.name,
          price:this.product.price,
          salePrice:this.product.salePrice,
          salePoint:this.product.salePoint
      }
      axios.put("http://localhost:3000/list/"+this.$route.params.id,newdata).then( res =>{
      // console.log('更新成功')
      // this.getIddata()
      this.$router.push('/example/products')
      },err =>{
        console.log('错误')
      })
    }
    // onCancel() {
    //   this.$message({
    //     message: 'cancel!',
    //     type: 'warning'
    //   })
    // },
    // getdata(id){
    //   axios.get(`http://localhost:3000/list/${id}`).then(res =>{
    //     console.log(res)
    //     // this.list = res.data.list
    //   })
    // }
  },
  created(){
    getIddata(this.$route.params.id).then( res=>{
      // console.log(res)
      this.product = res.data
    })
    
  }
}
</script>

<style scoped>
.line{
  text-align: center;
}
</style>

