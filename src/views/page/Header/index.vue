<template>
  <d2-container>
    <div style="margin: 20px;"></div>
    <el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
      <el-form-item label="nav1">
        <el-input v-model="formLabelAlign.nav1"></el-input>
      </el-form-item>
      <el-form-item label="nav2">
        <el-input v-model="formLabelAlign.nav2"></el-input>
      </el-form-item>
      <el-form-item label="nav3">
        <el-input v-model="formLabelAlign.nav3"></el-input>
      </el-form-item>
    </el-form>
  </d2-container>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      labelPosition: 'right',
      formLabelAlign: {
        nav1: '',
        nav2: '',
        nav3: ''
      }
    }
  },
  methods: {
  }
}
</script>

<style lang="scss" scoped>
  .el-input{
        width: 100%;
  }
  .el-form--label-right{
    display: flex;
  }
</style>
