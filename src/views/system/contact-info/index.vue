<template>
  <div class="manage">
    <el-dialog :title="dialogForm.type === 'add' ? '新增联系记录' : '更新联系记录'" :visible.sync="dialogForm.isShow">
      <el-form ref="form" label-width="100px" :model="dialogForm.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="联系对象姓名" prop="ciName">
            <el-select placeholder="请选择联系对象" v-model="dialogForm.formData.ciName" value-key="tid">
              <el-option v-for="option in dialogForm.candidateList" :key="option.tid" :label="option.tname"
                :value="option.tname" />
            </el-select>
          </el-form-item>
          <el-form-item label="联系类型" style="display:inline-block" prop="ciType">
            <el-select placeholder="请选择" v-model="dialogForm.formData.ciType">
              <el-option value="陌生寻访" />
              <el-option value="跟踪联系" />
              <el-option value="推荐记录" />
            </el-select>
          </el-form-item>
          <el-form-item label="人才状态" style="display:inline-block" prop="ciTalentstatus">
            <el-select placeholder="请选择" v-model="dialogForm.formData.ciTalentstatus">
              <el-option value="候选人" />
              <el-option value="人才推荐" />
              <el-option value="放弃" />
            </el-select>
          </el-form-item>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="所属项目" prop="ciProjectname">
            <el-select placeholder="请选择所属项目" v-model="dialogForm.formData.ciProjectname" value-key="pid">
              <el-option v-for="option in dialogForm.projectsList" :key="option.pid" :label="option.pname"
                :value="option.pname" />
                <el-option value="无" />
            </el-select>
          </el-form-item>
          <el-form-item label="请选择创建人" prop="ciCreator">
            <el-select placeholder="创建人" v-model="dialogForm.formData.ciCreator" value-key="id">
              <el-option v-for="option in dialogForm.staffList" :key="option.id" :label="option.name"
                :value="option.name" />
            </el-select>
          </el-form-item>

          <el-form-item label="联系日期" style="display:inline-block" prop="ciDate">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择联系日期"
              v-model="dialogForm.formData.ciDate" />
          </el-form-item>
          <el-form-item label="期望薪资" style="display:inline-block" prop="ciExpectedsalary">
            <el-select placeholder="请选择" v-model="dialogForm.formData.ciExpectedsalary">
              <el-option value="10k-15k" />
              <el-option value="15k-20k" />
              <el-option value="20k-25k" />
              <el-option value="25k-30k" />
              <el-option value="30k-35k" />
              <el-option value="35k-40k" />
              <el-option value="40k以上" />
            </el-select>
          </el-form-item>
        </el-form-item>
        <el-form-item label="期望工作地点" label-width="140px" style="width: 350px" prop="ciExpectedworkplace">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.ciExpectedworkplace" />
        </el-form-item>

        <el-form-item label="适合行业" label-width="140px" style="width: 350px" prop="ciSuitableindustry">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.ciSuitableindustry" />
        </el-form-item>
        <el-form-item label="适合职能" label-width="140px" style="width: 350px" prop="ciSuitableposition">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.ciSuitableposition" />
        </el-form-item>

        <el-form-item label-width="40px" style="margin-bottom:4px ">

          <el-form-item label="评语" style="width:450px" prop="ciComment">
            <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.ciComment"
              :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
          </el-form-item>
        </el-form-item>

      </el-form>

      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogForm.isShow = false">取消</el-button>
        <el-button type="primary" @click="confirm">确定</el-button>
      </div>
    </el-dialog>

    <!-- 点击查看详情后 -->
    <el-dialog title="联系记录详情" :visible.sync="contactInfoDialog.isShow">
      <el-form ref="form" label-width="100px" :model="contactInfoDialog.contactDetail" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px">
          <el-form-item label="适合行业" style="display:inline-block;width:300px" prop="ciSuitableindustry">
            <el-input readonly placeholder="" v-model.trim="contactInfoDialog.contactDetail.ciSuitableindustry" />
          </el-form-item>
          <el-form-item label="适合职能" style="display:inline-block;width:300px" prop="ciSuitableposition">
            <el-input readonly placeholder="" v-model.trim="contactInfoDialog.contactDetail.ciSuitableposition" />
          </el-form-item>
          <el-form-item label="期望薪资" style="display:inline-block;width:300px" prop="ciExpectedsalary">
            <el-input readonly placeholder="" v-model.trim="contactInfoDialog.contactDetail.ciExpectedsalary" />
          </el-form-item>
          <el-form-item label="评价" style="display:inline-block;width:500px" prop="ciComment">
            <el-input readonly type="textarea" :rows="4" placeholder=""
              v-model.trim="contactInfoDialog.contactDetail.ciComment" />
          </el-form-item>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="contactInfoDialog.isShow = false">取消</el-button>
        <el-button type="primary" @click="contactInfoDialog.isShow = false">确定</el-button>
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
        <el-form-item label="联系对象" prop="ciName">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.ciName" prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="联系类型" prop="ciType">
          <el-select placeholder="请选择类型" v-model="searchForm.formData.ciType">
            <el-option value="陌生寻访" />
            <el-option value="推荐记录" />
            <el-option value="跟踪联系" />
          </el-select>
        </el-form-item>
        <el-form-item label="人才状态" prop="ciTalentstatus">
          <el-select placeholder="请选择人才状态" v-model="searchForm.formData.ciTalentstatus">
            <el-option value="放弃" />
            <el-option value="人才推荐" />
            <el-option value="候选人" />
          </el-select>
        </el-form-item>
        <el-form-item label="联系日期" prop="ciDate">
          <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择起始日期"
            v-model="searchForm.formData.ciDate" />
        </el-form-item>
        <el-form-item label="创建人" style="display:inline-block" prop="ciCreator">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.ciCreator" prefix-icon="el-icon-search" />
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
        <el-table-column prop="ciId" label="ID" min-width="40" align="center" />
        <el-table-column prop="ciName" label="联系对象" min-width="160" align="center" />
        <el-table-column prop="ciType" label="联系类型" min-width="140" align="center" />
        <el-table-column prop="pstatus" label="人才状态" min-width="140" align="center" >
          <template slot-scope="scope">
                  <el-tag :type="scope.row.ciTalentstatus == '候选人' ? '' : scope.row.ciTalentstatus == '放弃'?'danger':'success'" disable-transitions>{{scope.row.ciTalentstatus }}
                  </el-tag>
              </template>
          </el-table-column>
        <el-table-column prop="ciProjectname" label="所属项目" min-width="200" align="center" />
        <el-table-column prop="ciExpectedworkplace" label="期望工作地点" min-width="125" align="center" />
        <el-table-column prop="ciDate" label="联系日期" min-width="125" align="center" />
        <el-table-column prop="ciCreator" label="创建人" min-width="80" align="center" />
        <el-table-column label="操作" width="280" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i>
            </el-button>
            <el-popconfirm style="margin-left:10px;margin-right:10px" confirm-button-text='确定' cancel-button-text='我再想想'
              icon="el-icon-info" icon-color="red" title="你确定删除吗？" @confirm="handleDelete(scope.row.ciId)">
              <el-button size="mini" type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i>
              </el-button>
            </el-popconfirm>
            <el-button type="warning" @click="getContactInfoDetail(scope.row.ciId)">查看详情 <i
                class="el-icon-user-solid" />
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
    getContactInfoList,
    getOne,
    add,
    getExportApi,
    getImportApi,
    edit
  } from '../../../api/contact-info.js'

  import {
    getAll
  } from '../../../api/staff'

  import {
    getOneProject,
    getAllProjects
  } from '../../../api/projects.js'

  import {
    getAllCandidate,
    editCandidate
  } from '../../../api/candidate.js'

  import {
    getAllCustomerContact,
    getOneCustomerContact
  } from '../../../api/customer-contact.js'

  import {
    createLogger,
    mapState
  } from 'vuex'

  export default {
    name: 'ContactInfo',
    data() {
      return {
        dialogForm: {
          type: 'add', // add为新增，edit为编辑
          isShow: false,
          projectsList: [],
          staffList: [],
          candidateList: [],
          formData: {}
        },
        searchForm: {
          deptList: [],
          formData: {}
        },
        contactInfoDialog: {
          isShow: false,
          contactDetail: [],
        },
        customerContactDialog: {
          type: "add",
          isShow: false,
          formData: {}
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
        contactinfoId: 0
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
      getCandidate() {
        // 获取所有部门
        getAllCandidate().then(response => {
          const list = []
          response.data.forEach(candidate => {
            list.push(candidate)
          })
          this.dialogForm.candidateList = list
          console.log(this.dialogForm.candidateList);
        })
      },
      getStaff() {
        getAll().then(response => {
          const list = []
          response.data.forEach(staff => {
            list.push(staff)
          })
          this.dialogForm.staffList = list
          // console.log(this.dialogForm.staffList);
        })
      },
      getProject() {
        getAllProjects().then(response => {
          const list = []
          response.data.forEach(projects => {
            list.push(projects)
          })
          this.dialogForm.projectsList = list
          console.log(this.dialogForm.projectsList);
        })
      },
      HandleEditCandidate(data){
        editCandidate({ttype:data.ciTalentstatus})
      },
      updateCustomerContact(e) {
        let ccid = e
        const list = []
        getAllCustomerContact().then(response => {
          if (response.code === 200) {
            console.log(ccid);
            console.log(response.data[ccid]);
            this.dialogForm.formData.pcustomercontact = response.data[ccid - 1].ccName
          } else {
            this.$message.error('错误！')
          }
        })
        this.$forceUpdate()
      },
      // 点击新增按钮，弹出对话框
      handleAdd() {
        this.dialogForm.isShow = true
        this.dialogForm.type = 'add'
        this.dialogForm.formData = {}
        this.getCandidate()
        this.getStaff()
        this.getProject()
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
        this.getCandidate()
        this.getStaff()
        this.getProject()
        this.HandleEditCandidate(this.dialogForm.formData)
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
              this.HandleEditCandidate(this.dialogForm.formData)
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
      // 加载所有部门数据
      loading() {
        getContactInfoList({
          current: this.table.pageConfig.current,
          size: this.table.pageConfig.size
        }, this.searchForm.formData).then(response => {
          if (response.code === 200) {
            this.table.tableTotal = response.data.list
            // console.log(response.data.list);
            this.table.pageConfig.total = response.data.total
          } else {
            this.$message.error(response.message)
          }
        })
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
      getContactInfoDetail(id) {
        this.contactinfoId = id
        getOne(this.contactinfoId).then(response => {
          if (response.code === 200) {
            this.contactInfoDialog.isShow = true
            this.contactInfoDialog.contactDetail = response.data
            console.log(this.contactInfoDialog.contactDetail);
          } else {
            this.$message.error('该客户还暂未添加联系人！')
            this.customerContactDialog.isShow = true
          }
        })
      }
    },
    created() {
      this.loading()
    }
  }
</script>
