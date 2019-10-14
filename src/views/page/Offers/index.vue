<template>
  <d2-container>
    <template slot="header">OfferList
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
      prop="newman"
      label="更新人"
      width="200">
    </el-table-column>
    <el-table-column
      prop="oldman"
      label="创建人"
      width="200">
    </el-table-column>
    <el-table-column
      prop="address"
      label="路径"
      width="200">
    </el-table-column>
    <el-table-column
      prop="title"
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
  name: 'Offers',
  methods: {
    handleClick (row) {
      console.log(row)
      this.$router.push(row.address)
    }
  },
  data () {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '2015 & 2016 Recruiting Seasons: August 2014 – June 2016',
        newman: 'xx',
        address: 'Offers1',
        oldman: 'xx',
        title: 'wstoffers'
      }, {
        date: '2016-05-04',
        name: '2017 Recruiting Season: August 2016 – June 2017',
        newman: 'xx',
        address: 'Offers2',
        oldman: 'xx',
        title: 'wstoffers'
      }, {
        date: '2016-05-04',
        name: '2018 Recruiting Season: June 2017 – June 2018',
        newman: 'xx',
        address: 'Offers3',
        oldman: 'xx',
        title: 'wstoffers'
      }, {
        date: '2016-05-04',
        name: '2019 Recruiting Season: April 2018 – Current (Updating)',
        newman: 'xx',
        address: 'Offers4',
        oldman: 'xx',
        title: 'wstoffers'
      }, {
        date: '2016-05-04',
        name: '2020 Recruiting Season: April 2019 – Current (Updating)',
        newman: 'xx',
        address: 'Offers5',
        oldman: 'xx',
        title: 'wstoffers'
      }]
    }
  }
}
</script>

<style scoped>
  .home-table{
    margin: 0 auto;
    margin-top: 30px;
  }
  .home-addapi{
    margin-left: 50px;
  }
</style>
