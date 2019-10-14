<template>
  <d2-container>
    <template slot="header">Home
      <el-button type="primary" class="home-addapi">添加接口</el-button>
    </template>
   
    <div class="home-table">
      <el-table
    :data="tableData"
    border
    style="width: 100%">
    <el-table-column
      fixed
      prop="date"
      label="更新日期"
      width="200">
    </el-table-column>
    <el-table-column
      prop="name"
      label="子页面名"
      width="240">
    </el-table-column>
    <el-table-column
      prop="province"
      label="更新人"
      width="200">
    </el-table-column>
    <el-table-column
      prop="city"
      label="创建人"
      width="200">
    </el-table-column>
    <el-table-column
      prop="address"
      label="路径"
      width="200">
    </el-table-column>
    <el-table-column
      prop="zip"
      label="标题"
      flex="1">
    </el-table-column>
    <el-table-column
      fixed="right"
      label="操作"
      width="200">
      <template slot-scope="scope">
        <el-button type="text" size="small">查看</el-button>
        <el-button type="text" size="small" @click="handleClick(scope.row)">编辑</el-button>
        <el-button type="text" size="small">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
    </div>
    
  </d2-container>
</template>

<script>
export default {
  name: 'Home',
   methods: {
      handleClick(row) {
        console.log(row)
        this.$router.push(row.name)
      }
    },
  data () {
    return {
      tableData: [{
        date: '2016-05-02',
        name: 'Home1',
        province: 'xx',
      }, {
        date: '2016-05-04',
        name: 'Home2',
        province: 'xx',
      }]
    }
  }
}
</script>

<style scoped>
  .home-table{
    margin: 0 auto;
    margin-top: 100px;
  }
  .home-addapi{
    margin-left: 50px;
  }
</style>