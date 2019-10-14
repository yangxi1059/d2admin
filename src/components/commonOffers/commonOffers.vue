<template>
    <d2-container>
        <template slot="header">2015 & 2016 Recruiting Seasons: August 2014 – June 2016</template>
        <el-form ref="form"  label-width="80px" style="margin-left:120px">
        <!-- 背景图地址 -->
        <el-input placeholder="offers背景图" v-model="input1" style="width:40%">
            <template slot="prepend">src</template>
        </el-input>
        <br/>
        <!-- 标题内容 -->
        <el-input placeholder="title" v-model="input2" style="width:40%;margin-top:20px;">
            <template slot="prepend">标题</template>
        </el-input>
        <br/>
        <el-button type="primary" @click="onSubmit" style="margin-top:30px">立即添加</el-button>
        <!-- 表格 -->
        <el-table
            :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)"
            stripe
            style="width: 100%;margin-top:30px"
            ref="clicktable"
            row-key="id"
            >
            <el-table-column
            prop="Mentee"
            label="Mentee"
            width="180">
            </el-table-column>
            <el-table-column
            prop="EducationBackground"
            label="Education background"
            width="250">
            </el-table-column>
            <el-table-column
            prop="OfferReceived"
            label="Offer received"
            width="180">
            </el-table-column>
            <el-table-column
            prop="Division"
            label="Division"
            width="180">
            </el-table-column>
            <el-table-column
            prop="ImgSrc"
            label="OfferImgsrc">
            </el-table-column>
            <el-table-column
            fixed="right"
            label="操作"
            width="100">
            <template slot-scope="scope">
                <el-button type="text" size="small" @click="handleClick(scope.$index,scope.row)">编辑</el-button>
                <el-button type="text" size="small" @click="handleDelete(scope.$index,tableData )">删除</el-button>
            </template>
            </el-table-column>
        </el-table>
        <!-- 表单分页器 -->
        <div class="block" style="margin:0 auto;margin-top:30px;width:50%">
            <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="currentPage"
            :page-sizes="[10, 15, 20, 25]"
            :page-size="10"
            layout="total, sizes, prev, pager, next, jumper"
            :total="total">
        </el-pagination>
        </div>
        <!-- 控制按钮 -->
        <el-button type="info" style="margin-right:100px;margin-top:30px">即时更新</el-button>
        <el-button type="danger" style="margin-top:30px">取消</el-button>
        </el-form>
        <!-- 数据添加弹出框 -->
        <el-dialog title="添加数据" :visible.sync="dialogVisible" width="30%">
          <el-form ref="form" label-width="80px">
            <el-form-item label="Mentee">
            <el-input v-model="form.mentee"></el-input>
            </el-form-item>
            <el-form-item label="Education">
            <el-input v-model="form.edu"></el-input>
            </el-form-item>
            <el-form-item label="Offer">
            <el-input v-model="form.offer"></el-input>
            </el-form-item>
            <el-form-item label="Division">
            <el-input v-model="form.division"></el-input>
            </el-form-item>
            <el-form-item label="ImgSrc">
            <el-input v-model="form.ImgSrc"></el-input>
            </el-form-item>
          </el-form>
          <span slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="gosumbit"
          >提交</el-button>
          </span>
        </el-dialog>
        <!-- 数据更新表单 -->
        <el-dialog
          title="编辑"
          :visible.sync="editFormVisible"
          >
          <el-form
          >
          <el-form-item
          label="Mentee"
          :label-width="formLabelWidth"
          >
          <el-input
          v-model="formchange.M"
          autocomplete="off"
          ></el-input>
          </el-form-item>
          <el-form-item
          label="Education"
          :label-width="formLabelWidth"
          >
          <el-input
          v-model="formchange.E"
          autocomplete="off"
          ></el-input>
          </el-form-item>
          <el-form-item
          label="OfferReceived"
          :label-width="formLabelWidth"
          >
          <el-input
          v-model="formchange.O"
          autocomplete="off"
          ></el-input>
          </el-form-item>
          <el-form-item
          label="Division"
          :label-width="formLabelWidth"
          >
          <el-input
          v-model="formchange.D"
          autocomplete="off"
          ></el-input>
          </el-form-item>
           <el-form-item
          label="ImgSrc"
          :label-width="formLabelWidth"
          >
          <el-input
          v-model="formchange.I"
          autocomplete="off"
          ></el-input>
          </el-form-item>
          </el-form>
          <div>
            <el-button @click="cancel()">取消</el-button>
            <el-button
              type="primary"
              v-on:click="sumbitEditRow()"
                >确定</el-button>
          </div>
        </el-dialog>
    </d2-container>
</template>

<script>
import Sortable from 'sortablejs'
var _index
export default {
  props: ['tableData'],
  data () {
    return {
      editFormVisible: false,
      formLabelWidth: '120px',
      name: '',
      total: '',
      currentPage: 1,
      pageSize: 10,
      input1: '',
      input2: '',
      dialogVisible: false,
      form: {
        mentee: '',
        edu: '',
        offer: '',
        division: '',
        ImgSrc: ''
      },
      formchange: {
        M: '',
        E: '',
        O: '',
        D: '',
        I: ''
      }
    }
  },
  created () {
    this.total = this.tableData.length
  },
  mounted () {
    this.setSort()
  },
  methods: {
    // 立即修改按钮弹出输入框
    onSubmit () {
      this.dialogVisible = true
    },
    // 编辑按钮弹出框表单默认值
    handleClick (index, row) {
      console.log(this.tableData.length)
      this.editFormVisible = true
      this.formchange.M = row.Mentee
      this.formchange.E = row.EducationBackground
      this.formchange.O = row.OfferReceived
      this.formchange.D = row.Division
      this.formchange.I = row.ImgSrc
      _index = index
    },
    // 编辑弹出框中的提交按钮
    sumbitEditRow () {
      var editData = _index
      this.tableData[editData].Mentee = this.formchange.M
      this.tableData[editData].EducationBackground = this.formchange.E
      this.tableData[editData].OfferReceived = this.formchange.O
      this.tableData[editData].Division = this.formchange.D
      this.tableData[editData].ImgSrc = this.formchange.I
      console.log(this.tableData)
      this.editFormVisible = false
    },
    // 编辑弹出框中的取消按钮
    cancel () {
      this.editFormVisible = false
    },
    // 动态改变每页 ${val} 条
    handleSizeChange (val) {
      this.pageSize = val
    },
    // 动态改变当前页数: ${val}
    handleCurrentChange (val) {
      this.currentPage = val
    },
    // 删除一行数据
    handleDelete (index, row) {
      console.log(index)
      this.$confirm('此操作将永久删除该数据, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.tableData.splice(index, 1)
        this.total = this.tableData.length
        this.$message({
          type: 'success',
          message: '删除成功!'
        })
      }).catch((err) => {
        this.$message({
          type: 'error',
          message: err
        })
      })
    },
    // 数据提交列表最后添加一条
    gosumbit () {
      this.tableData.unshift({
        Mentee: this.form.mentee,
        EducationBackground: this.form.edu,
        OfferReceived: this.form.offer,
        Division: this.form.division,
        ImgSrc: this.form.ImgSrc,
        id: this.tableData.length + 1
      })
      console.log(this.tableData)
      this.form.mentee = ''
      this.form.edu = ''
      this.form.offer = ''
      this.form.division = ''
      this.form.ImgSrc = ''
      this.dialogVisible = false
      this.total = this.tableData.length
    },
    setSort () {
      const el = this.$refs.clicktable.$el.querySelectorAll('.el-table__body-wrapper > table > tbody')[0]
      this.sortable = Sortable.create(el, {
        ghostClass: 'sortable-ghost',
        setData: function (dataTransfer) {
          dataTransfer.setData('Text', '')
        },
        onEnd: evt => {
          const targetRow = this.tableData.splice(evt.oldIndex, 1)[0]
          this.tableData.splice(evt.newIndex, 0, targetRow)
        }
      })
    }
  }
}
</script>

<style>
  .el-form-item__content{
    margin-top: 30px;
  }
</style>
