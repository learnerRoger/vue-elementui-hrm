<template>
  <div class="manage">
    <el-dialog :title="dialogForm.type === 'add' ? '新增候选人' : '更新候选人'" :visible.sync="dialogForm.isShow">
      <el-form ref="form" label-width="100px" :model="dialogForm.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="候选人姓名" style="display:inline-block;width:300px" prop="tname">
            <el-input placeholder="请输入姓名" v-model.trim="dialogForm.formData.tname" />
          </el-form-item>
          <el-form-item label="性别" style="display:inline-block" prop="tsex">
            <el-select placeholder="请选择" v-model="dialogForm.formData.tsex">
              <el-option value="男" />
              <el-option value="女" />
            </el-select>
          </el-form-item>
          <el-form-item label="年龄" style="display:inline-block;width:300px" prop="tage">
            <el-input placeholder="请输入年龄" v-model.trim="dialogForm.formData.tage" />
          </el-form-item>
          <el-form-item label="手机号码" style="display:inline-block;width:300px" prop="ttelephone">
            <el-input placeholder="请输入手机号码" v-model.trim="dialogForm.formData.ttelephone" />
          </el-form-item>
          <el-form-item label="专业" style="display:inline-block;width:300px" prop="tmajor">
            <el-input placeholder="请输入专业名称" v-model.trim="dialogForm.formData.tmajor" />
          </el-form-item>
          <el-form-item label="学历" style="display:inline-block" prop="teducation">
            <el-select placeholder="请选择学历" v-model="dialogForm.formData.teducation">
              <el-option value="本科" />
              <el-option value="硕士" />
              <el-option value="博士" />
            </el-select>
          </el-form-item>
          <el-form-item label="毕业学校" style="display:inline-block;width:300px" prop="tgraduateschool">
            <el-input placeholder="请输入学校名称" v-model.trim="dialogForm.formData.tgraduateschool" />
          </el-form-item>
          <el-form-item label="毕业时间" style="display:inline-block;width:300px" prop="tgraduatedate">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选毕业建时间"
              v-model="dialogForm.formData.tgraduatedate" />
          </el-form-item>
          <el-form-item label="工作年限" style="display:inline-block;width:300px" prop="texperience">
            <el-input placeholder="请输入工作年限" v-model.trim="dialogForm.formData.texperience" />
          </el-form-item>
          <el-form-item label="人才类别" style="display:inline-block;width:300px" prop="ttype">
            <el-select placeholder="请选择级别" v-model="dialogForm.formData.ttype">
              <el-option value="候选人" disabled/>
              <el-option value="人才推荐" />
              <el-option value="放弃" disabled/>
            </el-select>
          </el-form-item>
          <el-form-item label="人才级别" style="display:inline-block;width:300px" prop="tdegree">
            <el-select placeholder="请选择级别" v-model="dialogForm.formData.tdegree">
              <el-option value="员工" />
              <el-option value="主管" />
              <el-option value="经理" />
              <el-option value="总监" />
              <el-option value="副经理" />
              <el-option value="总经理" />
            </el-select>
          </el-form-item>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="婚姻状况" style="display:inline-block" prop="tmaritalstatus">
            <el-select placeholder="请选择婚姻状况" v-model="dialogForm.formData.tmaritalstatus">
              <el-option value="已婚" />
              <el-option value="未婚" />
            </el-select>
          </el-form-item>
          <el-form-item label="籍贯" style="display:inline-block;width:300px" prop="tnativeplace">
            <el-input placeholder="请输入籍贯" v-model.trim="dialogForm.formData.tnativeplace" />
          </el-form-item>
        </el-form-item>
        <el-form-item label="现居地" label-width="140px" style="width: 340px" prop="taddress">
          <el-input placeholder="请输入现居地" v-model.trim="dialogForm.formData.taddress" />
        </el-form-item>

        <el-form-item label="现任职公司" label-width="140px" style="width: 450px" prop="tcompany">
          <el-input placeholder="请输入现任职公司" v-model.trim="dialogForm.formData.tcompany" />
        </el-form-item>
        <el-form-item label="职位" label-width="140px" style="width: 450px" prop="tposition">
          <el-input placeholder="请输入职位" v-model.trim="dialogForm.formData.tposition" />
        </el-form-item>
        <el-form-item label="目前薪资" label-width="140px" style="width: 450px" prop="tsalary">
          <el-input placeholder="请输入目前薪资" v-model.trim="dialogForm.formData.tsalary" />
        </el-form-item>
        <el-form-item label="工作经历" label-width="140px" style="width: 450px" prop="tworkexperience">
          <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.tworkexperience"
            :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
        </el-form-item>
        <el-form-item label="项目经验" label-width="140px" style="width: 450px" prop="tprojectexperience">
          <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.tprojectexperience"
            :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
        </el-form-item>
        <el-form-item label="其他特长" label-width="140px" style="width: 450px" prop="totherability">
          <el-input placeholder="请输入其他特长" v-model.trim="dialogForm.formData.totherability" />
        </el-form-item>
        <el-form-item label="备注" label-width="140px" style="width: 450px" prop="tcomment">
          <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.tcomment"
            :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
        </el-form-item>
        <el-form-item label="创建人" label-width="140px" prop="tcreator">
          <el-select placeholder="创建人" v-model="dialogForm.formData.tcreator" value-key="id">
            <el-option v-for="option in dialogForm.staffList" :key="option.id" :label="option.cname"
              :value="option.name" />
          </el-select>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="创建时间" style="display:inline-block" prop="tCreatetime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择创建时间"
              v-model="dialogForm.formData.tCreatetime" />
          </el-form-item>
        </el-form-item>
      </el-form>

      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogForm.isShow = false">取消</el-button>
        <el-button type="primary" @click="confirm">确定</el-button>
      </div>
    </el-dialog>

    <!-- 点击查看详情后后 -->
    <el-dialog title="人才详情" :visible.sync="customerDialog.isShow">
      <el-form ref="form" label-width="100px" :model="customerDialog.contactDetail" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px">
          <el-form-item label="现任职公司" style="display:inline-block;width:300px" prop="tcompany">
            <el-input readonly="true" placeholder="" v-model.trim="customerDialog.contactDetail.tcompany"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="职位" style="display:inline-block;width:300px" prop="tposition">
            <el-input readonly="true" placeholder="" v-model.trim="customerDialog.contactDetail.tposition"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="现居住地" style="display:inline-block;width:300px" prop="taddress">
            <el-input readonly="true" placeholder="" v-model.trim="customerDialog.contactDetail.taddress"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="籍贯" style="display:inline-block;width:300px" prop="tnativeplace">
            <el-input readonly="true" placeholder="" v-model.trim="customerDialog.contactDetail.tnativeplace"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="婚姻状态" style="display:inline-block;width:300px" prop="tmaritalstatus">
            <el-input readonly="true" placeholder="" v-model.trim="customerDialog.contactDetail.tmaritalstatus"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="工作经历" style="display:inline-block;width:500px" prop="tworkexperience">
            <el-input readonly="true" type="textarea" :rows="4" placeholder=""
              v-model.trim="customerDialog.contactDetail.tworkexperience" contenteditable="false" />
          </el-form-item>
          <el-form-item label="项目经验" style="display:inline-block;width:500px" prop="tprojectexperience">
            <el-input readonly="true" type="textarea" :rows="4" placeholder=""
              v-model.trim="customerDialog.contactDetail.tprojectexperience" contenteditable="false" />
          </el-form-item>
          <el-form-item label="其他特长" style="display:inline-block;width:500px" prop="totherability">
            <el-input readonly="true" type="textarea" :rows="4" placeholder=""
              v-model.trim="customerDialog.contactDetail.totherability" contenteditable="false" />
          </el-form-item>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="customerDialog.isShow = false">取消</el-button>
        <el-button type="primary" @click="customerDialog.isShow = false">确定</el-button>
      </div>
    </el-dialog>


    <div style="margin-bottom: 10px">
      <el-upload :action="importApi" :headers="headers" accept="xlsx" :show-file-list="false"
        :on-success="handleImportSuccess" :multiple="false" style="display:inline-block;">
        <el-button type="success" size="mini">导入 <i class="el-icon-bottom"></i>
        </el-button>
      </el-upload>
      <el-button type="warning" size="mini" @click="exportData" style="margin-left: 10px">导出 <i class="el-icon-top"></i>
      </el-button>
      <el-button type="primary" @click="handleAdd" size="mini">新增 <i class="el-icon-circle-plus-outline"></i>
      </el-button>
      <el-popconfirm style="margin-left: 10px" confirm-button-text='确定' cancel-button-text='我再想想' icon="el-icon-info"
        icon-color="red" title="你确定删除吗？" @confirm="handleDeleteBatch">
        <el-button type="danger" size="mini" slot="reference">批量删除 <i class="el-icon-remove-outline"></i>
        </el-button>
      </el-popconfirm>

    </div>

    <!------------------------- 搜索 ------------------------------------>
    <div class="manage-header">
      <el-form label-width="auto" :model="searchForm.formData" :inline="true" size="mini">

        <el-form-item label="人才姓名" prop="tname">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.tname" prefix-icon="el-icon-search" />
        </el-form-item>

        <el-form-item label="专业" prop="tmajor">
          <el-input placeholder="请输入专业" v-model.trim="searchForm.formData.tmajor" prefix-icon="el-icon-search" />
        </el-form-item>

        <el-form-item label="人才类别" style="display:inline-block" prop="ttype">
          <el-select placeholder="请选择类型" v-model="searchForm.formData.ttype">
            <el-option value="客户联系人" />
            <el-option value="候选人" />
          </el-select>
        </el-form-item>

        <el-form-item label="学历" prop="teducation">
          <el-select placeholder="请选择" v-model="searchForm.formData.teducation">
            <el-option label="本科" value="本科" />
            <el-option label="硕士" value="硕士" />
            <el-option label="博士" value="博士" />
          </el-select>
        </el-form-item>

        <el-form-item label="人才级别" prop="tdegree">
          <el-select placeholder="请选择" v-model="searchForm.formData.tdegree">
            <el-option value="员工" />
            <el-option value="主管" />
            <el-option value="经理" />
            <el-option value="总监" />
            <el-option value="副经理" />
            <el-option value="总经理" />
          </el-select>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="search" size="mini">搜索 <i class="el-icon-search" /></el-button>
          <el-button type="danger" @click="reset" size="mini">重置 <i class="el-icon-refresh-left" /></el-button>
        </el-form-item>

      </el-form>
    </div>
    <div class="common-table">
      <el-table :data="table.tableTotal" height="85%" border stripe row-key="id" :header-cell-style="{background: '#eef1f6',color: '#606266',
        textAlign:'center',fontWeight:'bold',borderWidth:'3px'}" @selection-change="handleSelectionChange">
        <el-table-column type="selection" width="50" align="center" />
        <el-table-column prop="tid" label="ID" min-width="40" align="center" />
        <el-table-column prop="tname" label="姓名" min-width="100" align="center" />
        <el-table-column prop="tsex" label="性别" min-width="50" align="center" />
        <el-table-column prop="tage" label="年龄" min-width="50" align="center" />
        <el-table-column prop="ttelephone" label="手机号码" min-width="140" align="center" />
        <el-table-column prop="tgraduateschool" label="毕业院校" min-width="150" align="center" />
        <el-table-column prop="tmajor" label="专业" min-width="180" align="center" />
        <el-table-column prop="teducation" label="学历" min-width="60" align="center" />
        <!-- <el-table-column prop="pstatus" label="人才类别" min-width="140" align="center" >
          <template slot-scope="scope">
                  <el-tag :type="scope.row.ttype == '候选人' ? '' : scope.row.ttype == '放弃'?'danger':'success'" disable-transitions>{{scope.row.ttype }}
                  </el-tag>
              </template>
          </el-table-column> -->
        <el-table-column prop="tcreatetime" label="创建时间" min-width="155" align="center" />
        <el-table-column prop="tcreator" label="登记人" min-width="125" align="center" />
        <el-table-column prop="tdegree" label="人才级别" min-width="90" align="center" />
        <el-table-column prop="tcomment" label="备注" min-width="200" align="center" />
        <el-table-column label="操作" width="280" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i>
            </el-button>
            <el-popconfirm style="margin-left:10px;margin-right:10px" confirm-button-text='确定' cancel-button-text='我再想想'
              icon="el-icon-info" icon-color="red" title="你确定删除吗？" @confirm="handleDelete(scope.row.cid)">
              <el-button size="mini" type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i>
              </el-button>
            </el-popconfirm>
            <el-button type="warning" @click="getCandidateDetail(scope.row.tid)">查看详情 <i class="el-icon-user-solid" />
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-pagination class="pager" layout="total,sizes,prev,pager,next,jumper"
        :page-size="table.pageConfig.size ? table.pageConfig.size : 10" :page-sizes="[5, 10, 15, 20]"
        :total="table.pageConfig.total" :current-page.sync="table.pageConfig.current" @size-change="handleSizeChange"
        @current-change="handleCurrentChange"></el-pagination>
    </div>
  </div>
</template>
<script>
  import {
    deleteBatch,
    deleteOne,
    getCandidateList,
    getOne,
    add,
    getExportApi,
    getImportApi,
    edit
  } from '../../../api/candidate'

  import {
    getAllProjects
  } from '../../../api/projects'

  import {
    getAll
  } from '../../../api/staff.js'
  import {
    getAllDept
  } from '../../../api/dept.js'

  import {
    createLogger,
    mapState
  } from 'vuex'

  export default {
    name: 'Candidate',
    data() {
      return {
        dialogForm: {
          type: 'add', // add为新增，edit为编辑
          isShow: false,
          typeList: ["客户联系人", "候选人"],
          ccompanyTypeList: [],
          staffList: [],
          formData: {}
        },
        searchForm: {
          deptList: [],
          formData: {}
        },
        customerDialog: {
          isShow: false,
          contactDetail: [],
        },
        table: {
          tableData: [],
          tableDataContact: [],
          tableDataContracts: [],
          tableTotal: [],
          pageConfig: {
            total: 10, // 记录总数
            current: 1, // 起始页
            size: 10 // 每页展示的记录数
          }
        },
        ids: [],
        candidateId: 0
      }
    },
    computed: {
      ...mapState('token', ['token']),
      headers() {
        return {
          token: this.token
        }
      },
      // 获取导入数据的接口
      importApi() {
        return getImportApi()
      }
    },
    methods: {
      getDept() {
        // 获取所有部门
        getAllDept().then(response => {
          const list = []
          response.data.forEach(dept => {
            if (dept.children.length > 0) {
              dept.disabled = true
              list.push(dept)
              dept.children.forEach(subDept => {
                list.push(subDept)
              })
            }
          })
          this.dialogForm.deptList = list
        })
      },
      getStaff() {
        getAll().then(response => {
          const list = []
          response.data.forEach(staff => {
            list.push(staff)
          })
          this.dialogForm.staffList = list
          console.log(this.dialogForm.staffList);
        })
      },

      // 点击新增按钮，弹出对话框
      handleAdd() {
        this.dialogForm.isShow = true
        this.dialogForm.type = 'add'
        this.dialogForm.formData = {}
        this.getDept()
        this.getStaff()
      },
      handleDelete(id) {
        deleteOne(id).then(
          response => {
            if (response.code === 200) {
              this.$message.success('删除成功！')
              this.loading()
            } else {
              this.$message.error('删除失败！')
            }
          }
        )
      },
      handleDeleteBatch() {
        deleteBatch(this.ids).then(response => {
          if (response.code === 200) {
            this.$message.success('批量删除成功！')
            this.loading()
          } else {
            this.$message.error('批量删除失败！')
          }
        })
      },
      handleEdit(row) {
        this.dialogForm.isShow = true
        this.dialogForm.type = 'edit'
        this.dialogForm.formData = row
        this.getDept()
      },
      confirm() {
        // 通过type来判断是新增还是编辑
        if (this.dialogForm.type === 'add') {
          add(this.dialogForm.formData).then((response) => {
            if (response.code === 200) {
              this.$message.success('添加成功！')
              this.dialogForm.isShow = false
              this.loading()
            } else {
              this.$message.error('添加失败！')
            }
          })
        } else {
          edit(this.dialogForm.formData).then((response) => {
            if (response.code === 200) {
              this.$message.success('修改成功！')
              this.dialogForm.isShow = false
              this.loading()
            } else {
              this.$message.error('修改失败！')
            }
          })
        }
      },
      search() {
        this.loading()
      },
      // 重置搜索表单
      reset() {
        this.searchForm.formData = {}
        this.loading()
      },
      handleSizeChange(size) {
        this.table.pageConfig.size = size
        this.loading()
      },
      handleCurrentChange(current) {
        this.table.pageConfig.current = current
        this.loading()
      },
      handleSelectionChange(list) {
        this.ids = list.map(item => item.id)
      },
      handleStatusChange(row) {
        edit(row)
      },
      // 加载候选人数据
      loading() {
        getCandidateList({
          current: this.table.pageConfig.current,
          size: this.table.pageConfig.size
        }, this.searchForm.formData).then(response => {
          if (response.code === 200) {
            console.log(response.data);
            this.table.tableTotal = response.data.list
            this.table.pageConfig.total = response.data.total
          } else {
            this.$message.error(response.message)
          }
        })
        this.getStaff()
      },

      // 导出数据
      exportData() {
        window.open(getExportApi())
      },
      handleImportSuccess(response) {
        if (response.code === 200) {
          this.$message.success('数据导入成功！')
          this.loading()
        } else {
          this.$message.error('数据导入失败！')
        }
      },
      getCandidateDetail(id) {
        this.candidateId = id
        getOne(this.candidateId).then(response => {
          if (response.code === 200) {
            this.customerDialog.isShow = true
            this.customerDialog.contactDetail = response.data
            console.log(this.customerDialog.contactDetail);
          } else {
            this.$message.error('获取人才详情失败！')
          }
        })
      }
    },
    created() {
      this.loading()
    }
  }
</script>
