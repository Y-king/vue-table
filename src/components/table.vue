<template>
  <div class="tablebox">
    <!-- 表格 -->
    <el-table
      :data="dataList"
      style="width: 100%"
      border
      stripe
      :default-sort = "{prop: 'birthdate', order: 'descending'}"
      >
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="姓名">
              <span>{{ props.row.name }}</span>
            </el-form-item>
            <el-form-item label="昵称">
              <span>{{ props.row.nickname }}</span>
            </el-form-item>
            <el-form-item label="年龄">
              <span>{{ props.row.age }}</span>
            </el-form-item>
            <el-form-item label="邮箱">
              <span>{{ props.row.email }}</span>
            </el-form-item>
            <el-form-item label="地址">
              <span>{{ props.row.address.line1 }}</span>
            </el-form-item>
          </el-form>
        </template>
      </el-table-column>

      <el-table-column
        prop="name"
        label="姓名">
      </el-table-column>

      <el-table-column
        prop="email"
        label="邮箱">
      </el-table-column>

      <el-table-column
        prop="nickname"
        label="昵称">
      </el-table-column>

      <el-table-column
        prop="birthdate"
        label="生日"
        sortable>
      </el-table-column>

      <el-table-column
        prop="gender"
        label="性别">
      </el-table-column>
    </el-table>
    <!-- 分页 -->
    <pagination @pageChange="pageChange" :total="total" :currentPage = "curPage"></pagination>
  </div>
</template>

<script>
  import pagination from './page.vue';

  export default {
    components:{
      "pagination":pagination
    },
    data(){
      return{
        dataList:[],
        curPage: 1, //当前的页数
        total:0     //数据的总数
      }
    },
    methods:{
      getData(val){
        let self = this;
        let url = '/users';
        self.$axios({
            method:'get',
            url:url,
            params: {
              page:val
            }
        }).then(res=>{
            self.dataList = res.data.data;
            self.curPage = res.data.current_page;
            self.total = res.data.total;
        }).catch(err=>{
            console.log(err)
        })
      },    
      pageChange(val){
        this.getData(val);
      }
    },
    mounted(){
      this.getData(1);
    }
  }
</script>
<style lang="css" scoped>
  .el-form-item{display: block; text-align: left;}
</style>