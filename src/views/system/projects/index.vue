<template>
  <div class="manage">
    <el-dialog :title="dialogForm.type === 'add' ? '新增项目' : '更新项目'" :visible.sync="dialogForm.isShow">
      <el-form ref="form" label-width="100px" :model="dialogForm.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="项目名称" style="display:inline-block;width:300px" prop="pname">
            <el-input placeholder="请输入名称" v-model.trim="dialogForm.formData.pname" />
          </el-form-item>
          <el-form-item label="项目状态" style="display:inline-block" prop="pstatus">
            <el-select placeholder="请选择" v-model="dialogForm.formData.pstatus">
              <el-option value="进行中" />
              <el-option value="已完成" />
              <el-option value="暂停中" />
            </el-select>
          </el-form-item>
          <el-form-item label="优先级别" style="display:inline-block" prop="ppriority">
            <el-select placeholder="请选择" v-model="dialogForm.formData.ppriority">
              <el-option value="低" />
              <el-option value="中" />
              <el-option value="高" />
              <el-option value="极高" />
            </el-select>
          </el-form-item>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="客户名称" prop="pcustomername">
            <el-select placeholder="请选择客户" v-model="dialogForm.formData.pcustomername" value-key="cid"
              @change="updateCustomerContact">
              <el-option v-for="option in dialogForm.deptList" :key="option.cid" :label="option.cname"
                :value="option.cname" />
            </el-select>
          </el-form-item>
          <el-form-item label="主要顾问" prop="pconsultant">
            <el-select placeholder="请选择顾问" v-model="dialogForm.formData.pconsultant" value-key="id">
              <el-option v-for="option in dialogForm.staffList" :key="option.id" :label="option.cname"
                :value="option.name" />
            </el-select>
          </el-form-item>
          <el-form-item label="创建时间" style="display:inline-block" prop="pstarttime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择时间"
              v-model="dialogForm.formData.pstarttime" />
          </el-form-item>
          <el-form-item label="预期完成时间" style="display:inline-block" prop="pexpectedcompletetime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择时间"
              v-model="dialogForm.formData.pexpectedcompletetime" />
          </el-form-item>
        </el-form-item>
        <el-form-item label="客户联系人" label-width="140px" style="width: 350px" prop="pcustomercontact">
          <el-input readonly placeholder="请输入" v-model.trim="dialogForm.formData.pcustomercontact" />
        </el-form-item>
        <el-form-item label="工作地点" label-width="140px" style="width: 350px" prop="pworkplace">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.pworkplace" />
        </el-form-item>
        <el-form-item label="行业" label-width="140px" style="width: 350px" prop="pindustry">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.pindustry" />
        </el-form-item>
        <el-form-item label="适合职能" label-width="140px" style="width: 350px" prop="psuitableposition">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.psuitableposition" />
        </el-form-item>
        <el-form-item label="外语要求" label-width="140px" style="width: 350px" prop="planguagerequirement">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.planguagerequirement" />
        </el-form-item>

        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="年龄要求" style="display:inline-block" prop="pagerequirement">
            <el-select placeholder="请选择" v-model="dialogForm.formData.pagerequirement">
              <el-option value="25以上" />
              <el-option value="25-30" />
              <el-option value="30-35" />
              <el-option value="35-40" />
              <el-option value="40以下" />
            </el-select>
          </el-form-item>
          <el-form-item label="性别要求" style="display:inline-block" prop="psexrequirement">
            <el-select placeholder="请选择" v-model="dialogForm.formData.psexrequirement">
              <el-option value="不限" />
              <el-option value="男" />
              <el-option value="女" />
            </el-select>
          </el-form-item>
          <el-form-item label="学历要求" style="display:inline-block" prop="peducationrequirement">
            <el-select placeholder="请选择" v-model="dialogForm.formData.peducationrequirement">
              <el-option value="不限" />
              <el-option value="本科及以上" />
              <el-option value="硕士及以上" />
              <el-option value="博士及以上" />
            </el-select>
          </el-form-item>
          <el-form-item label="薪资范围" style="display:inline-block" prop="psalaryrange">
            <el-select placeholder="请选择类型" v-model="dialogForm.formData.psalaryrange">
              <el-option value="10k-15k" />
              <el-option value="15k-20k" />
              <el-option value="20k-25k" />
              <el-option value="25k-30k" />
              <el-option value="30k-35k" />
              <el-option value="35k-40k" />
              <el-option value="40k以上" />
            </el-select>
          </el-form-item>
          <el-form-item label="福利" style="width:450px" prop="pwelfare">
            <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.pwelfare"
              :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
          </el-form-item>
          <el-form-item label="职位描述" style="width:450px" prop="ppositiondescription">
            <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.ppositiondescription"
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
    <el-dialog title="项目详情" :visible.sync="projectDialog.isShow">
      <el-form ref="form" label-width="100px" :model="projectDialog.contactDetail" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px">
          <el-form-item label="适合职能" style="display:inline-block;width:300px" prop="psuitableposition">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.psuitableposition"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="性别要求" style="display:inline-block;width:300px" prop="psexrequirement">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.psexrequirement"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="外语要求" style="display:inline-block;width:300px" prop="planguagerequirement">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.planguagerequirement"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="学历要求" style="display:inline-block;width:300px" prop="peducationrequirement">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.peducationrequirement"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="职位级别" style="display:inline-block;width:300px" prop="ppositoinlevel">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.ppositoinlevel"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="年龄要求" style="display:inline-block;width:300px" prop="pagerequirement">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.pagerequirement"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="职位描述" style="display:inline-block;width:300px" prop="ppositiondescription">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.ppositiondescription"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="薪资范围" style="display:inline-block;width:300px" prop="psalaryrange">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.psalaryrange"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="福利" style="display:inline-block;width:300px" prop="pwelfare">
            <el-input readonly placeholder="" v-model.trim="projectDialog.contactDetail.pwelfare"
              contenteditable="false" />
          </el-form-item>
          <el-form-item label="客户简介" style="display:inline-block;width:500px" prop="pcompanyintroduction">
            <el-input readonly type="textarea" :rows="4" placeholder=""
              v-model.trim="projectDialog.contactDetail.pcompanyintroduction" contenteditable="false" />
          </el-form-item>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="projectDialog.isShow = false">取消</el-button>
        <el-button type="primary" @click="projectDialog.isShow = false">确定</el-button>
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
        <el-form-item label="项目名称" prop="pname">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.pname" prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="客户名称" prop="pcustomername">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.pcustomername" prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="状态" prop="pstatus">
          <el-select placeholder="请选择类型" v-model="searchForm.formData.pstatus">
            <el-option value="进行中" />
            <el-option value="已完成" />
            <el-option value="暂停中" />
          </el-select>
        </el-form-item>
        <el-form-item label="主要顾问" style="display:inline-block" prop="pconsultant">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.pconsultant" prefix-icon="el-icon-search" />
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
        <el-table-column prop="pid" label="ID" min-width="40" align="center" />
        <el-table-column prop="pname" label="项目名称" min-width="160" align="center" />
        <el-table-column prop="pcustomername" label="客户名称" min-width="240" align="center" />
        <el-table-column prop="pworkplace" label="城市" min-width="100" align="center" />
        <el-table-column prop="pconsultant" label="主要顾问" min-width="100" align="center" />
        <el-table-column prop="pcustomercontact" label="客户联系人" min-width="125" align="center" />
        <el-table-column prop="pstarttime" label="创建时间" min-width="125" align="center" />
        <el-table-column prop="pexpectedcompletetime" label="预期结束时间" min-width="125" align="center" />
        <el-table-column prop="pstatus" label="项目状态" min-width="140" align="center" >
          <template slot-scope="scope">
                  <el-tag :type="scope.row.pstatus == '进行中' ? '' : scope.row.pstatus == '暂停中'?'danger':'success'" disable-transitions>{{scope.row.pstatus }}
                  </el-tag>
              </template>
          </el-table-column>
        <el-table-column prop="ppriority" label="优先级别" min-width="80" align="center" />
        <el-table-column label="操作" width="280" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i>
            </el-button>
            <el-popconfirm style="margin-left:10px;margin-right:10px" confirm-button-text='确定' cancel-button-text='我再想想'
              icon="el-icon-info" icon-color="red" title="你确定删除吗？" @confirm="handleDelete(scope.row.pid)">
              <el-button size="mini" type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i>
              </el-button>
            </el-popconfirm>
            <el-button type="warning" @click="getProjectDetail(scope.row.pid)">查看详情 <i class="el-icon-user-solid" />
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
    getProjectsList,
    getOne,
    add,
    getExportApi,
    getImportApi,
    edit
  } from '../../../api/projects'

  import {
    getAll
  } from '../../../api/staff'

  import {
    getOneProject
  } from '../../../api/projects.js'

  import {
    getAllCustomer
  } from '../../../api/customer.js'

  import {
    getAllCustomerContact,
    getOneCustomerContact
  } from '../../../api/customer-contact.js'

  import {
    createLogger,
    mapState
  } from 'vuex'

  export default {
    name: 'Customer',
    data() {
      return {
        dialogForm: {
          type: 'add', // add为新增，edit为编辑
          isShow: false,
          deptList: [],
          staffList: [],
          ccompanyTypeList: [],
          formData: {}
        },
        searchForm: {
          deptList: [],
          formData: {}
        },
        projectDialog: {
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
        projectId: 0
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
      getCustomer() {
        // 获取所有部门
        getAllCustomer().then(response => {
          const list = []
          response.data.forEach(customer => {
            list.push(customer)
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
        this.getCustomer()
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
        this.getCustomer()
        this.getStaff()
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
      // 加载所有部门数据
      loading() {
        getProjectsList({
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
      confirmCC() {
        addCC(this.customerContactDialog.formData).then((response) => {
          if (response.code === 200) {
            this.$message.success('添加成功！')
            this.customerContactDialog.isShow = false
            this.loading()
          } else {
            this.$message.error('添加失败！')
          }
        })
      },
      getProjectDetail(id) {
        this.projectId = id
        getOneProject(this.projectId).then(response => {
          if (response.code === 200) {
            this.projectDialog.isShow = true
            this.projectDialog.contactDetail = response.data
            console.log(this.projectDialog.contactDetail);
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
