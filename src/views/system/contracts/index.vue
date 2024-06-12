<template>
  <div class="manage">
    <el-dialog :title="dialogForm.type == 'download' ? '下载合同' : dialogForm.type == 'add'?'新增合同':'编辑合同'"
      :visible.sync="dialogForm.isShow">
      <el-form ref="form" label-width="100px" :model="dialogForm.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="合同名称" style="display:inline-block;width:300px" prop="pname">
            <el-input placeholder="请输入名称" v-model.trim="dialogForm.formData.conName" />
          </el-form-item>
          <el-form-item label="关联项目名称" style="display:inline-block" prop="conProjectname">
            <el-select placeholder="请选择项目" v-model="dialogForm.formData.conProjectname" value-key="pid">
              <el-option v-for="option in dialogForm.projectsList" :key="option.pid" :label="option.pname"
                :value="option.pname" />
            </el-select>
          </el-form-item>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="客户名称" prop="conCustomname">
            <el-select placeholder="请选择客户" v-model="dialogForm.formData.conCustomname" value-key="cid"
              @change="updateCustomerContact">
              <el-option v-for="option in dialogForm.deptList" :key="option.cid" :label="option.cname"
                :value="option.cname" />
            </el-select>
          </el-form-item>
          <el-form-item label="公司签约人" prop="conCompanycontractor">
            <el-select placeholder="创建人" v-model="dialogForm.formData.conCompanycontractor" value-key="id">
              <el-option v-for="option in dialogForm.staffList" :key="option.id" :label="option.name"
                :value="option.name" />
            </el-select>
          </el-form-item>
          <el-form-item label="客户签约人" style="display:inline-block;width:300px" prop="conCustomercontractor">
            <el-input placeholder="请输入名称" v-model.trim="dialogForm.formData.conCustomercontractor" />
          </el-form-item>
          <el-form-item label="签约时间" style="display:inline-block" prop="conSigndate">
            <el-date-picker type="datetime" value-format="yyyy-MM-dd HH:mm:ss" placeholder="请选择时间"
              v-model="dialogForm.formData.conSigndate" />
          </el-form-item>
          <el-form-item label="签约地点" style="display:inline-block" prop="conSignaddress">
            <el-input placeholder="请输入地点" v-model.trim="dialogForm.formData.conSignaddress" />
          </el-form-item>
          <el-form-item label="项目开始时间" style="display:inline-block" prop="conStarttime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择时间"
              v-model="dialogForm.formData.conStarttime" />
          </el-form-item>
          <el-form-item label="项目结束时间" style="display:inline-block" prop="conEndtime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择时间"
              v-model="dialogForm.formData.conEndtime" />
          </el-form-item>
        </el-form-item>
        <el-form-item label="金额" label-width="140px" style="width: 350px" prop="conAmount">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.conAmount" />
        </el-form-item>
        <el-form-item label="付款状态" label-width="140px" style="display:inline-block" prop="conStatus">
          <el-select placeholder="请选择" v-model="dialogForm.formData.conStatus">
            <el-option value="未付款" />
            <el-option value="已付款" />
            <el-option value="未结项" />
          </el-select>
        </el-form-item>
        </el-form-item>

      </el-form>

      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogForm.isShow = false">取消</el-button>
        <el-button type="primary" @click="confirm">确定</el-button>
      </div>
    </el-dialog>

    <!-- 点击查看详情后 -->
    <!-- <el-dialog title="项目详情" :visible.sync="projectDialog.isShow">
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
    </el-dialog> -->


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
        <el-form-item label="合同名称" prop="conName">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.conName" prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="客户名称" prop="conCustomname">
          <el-select placeholder="请选择客户" v-model="searchForm.formData.conCustomname" value-key="cid">
            <el-option v-for="option in dialogForm.deptList" :key="option.cid" :label="option.cname"
              :value="option.cname" />
          </el-select>
        </el-form-item>
        <el-form-item label="项目名称" style="display:inline-block" prop="conProjectname">
          <el-select placeholder="请选择项目" v-model="searchForm.formData.conProjectname" value-key="pid">
            <el-option v-for="option in dialogForm.projectsList" :key="option.pid" :label="option.pname"
              :value="option.pname" />
          </el-select>
        </el-form-item>
        <el-form-item label="付款状态" prop="conStatus">
          <el-select placeholder="请选择类型" v-model="searchForm.formData.conStatus">
            <el-option value="已付款" />
            <el-option value="未付款" />
            <el-option value="未结项" />
          </el-select>
        </el-form-item>
        <el-form-item label="公司签约人" prop="conCompanycontractor">
          <el-select placeholder="请选择" v-model="searchForm.formData.conCompanycontractor" value-key="id">
            <el-option v-for="option in dialogForm.staffList" :key="option.id" :label="option.name"
              :value="option.name" />
          </el-select>
        </el-form-item>
        <el-form-item label="客户签约人" style="display:inline-block;width:300px" prop="conCustomercontractor">
          <el-input placeholder="请输入名称" v-model.trim="searchForm.formData.conCustomercontractor" />
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
        <el-table-column prop="conId" label="ID" min-width="40" align="center" />
        <el-table-column prop="conName" label="合同名称" min-width="160" align="center" />
        <el-table-column prop="conCustomname" label="客户名称" min-width="240" align="center" />
        <el-table-column prop="conProjectname" label="项目名称" min-width="240" align="center" />
        <el-table-column prop="conCompanycontractor" label="公司签约人" min-width="100" align="center" />
        <el-table-column prop="conCustomercontractor" label="客户签约人" min-width="100" align="center" />
        <el-table-column prop="conSigndate" label="签约时间" min-width="180" align="center" />
        <el-table-column prop="conStarttime" label="项目开始时间" min-width="125" align="center" />
        <el-table-column prop="conEndtime" label="项目结束时间" min-width="125" align="center" />
        <el-table-column prop="conAmount" label="金额" min-width="125" align="center" />
        <el-table-column prop="conStatus" label="付款状态" min-width="140" align="center">
          <template slot-scope="scope">
            <el-tag :type="scope.row.conStatus == '未付款' ? '' : scope.row.conStatus == '未结项'?'danger':'success'"
              disable-transitions>{{scope.row.conStatus }}
            </el-tag>
          </template>
        </el-table-column>
        <el-table-column label="操作" width="280" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i>
            </el-button>
            <el-popconfirm style="margin-left:10px;margin-right:10px" confirm-button-text='确定' cancel-button-text='我再想想'
              icon="el-icon-info" icon-color="red" title="你确定删除吗？" @confirm="handleDelete(scope.row.conId)">
              <el-button size="mini" type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i>
              </el-button>
            </el-popconfirm>
            <el-button type="warning" @click="handleDownload(scope.row)">下载合同 <i class="el-icon-download" />
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
    getContractsLst,
    getOne,
    add,
    getAllContracts,
    getExportApi,
    getImportApi,
    edit,
    down
  } from '../../../api/contracts.js'

  import {
    getAll
  } from '../../../api/staff'

  import {
    getOneProject,
    getAllProjects
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
    name: 'Contracts',
    data() {
      return {
        dialogForm: {
          type: 'add', // add为新增，edit为编辑
          isShow: false,
          deptList: [],
          staffList: [],
          projectsList: [],
          contractsLst: [],
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
        contractId: 0
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
        // 获取所有客户
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
          // console.log(this.dialogForm.staffList);
        })
      },
      getContracts() {
        getAllContracts().then(response => {
          const list = []
          response.data.forEach(contracts => {
            list.push(contracts)
          })
          this.dialogForm.contractsLst = list
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
          // console.log(this.dialogForm.projectsList);
        })
      },
      updateCustomerContact(e) {
        let ccid = e
        const list = []
        getAllCustomerContact().then(response => {
          if (response.code === 200) {
            console.log(ccid);
            // console.log(response.data[ccid]);
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
        this.getProject()
        this.getContracts()
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
      handleDownload(row) {
        this.dialogForm.isShow = true
        this.dialogForm.formData = row
        this.dialogForm.type = 'download'
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
        } else if (this.dialogForm.type === 'edit') {
          edit(this.dialogForm.formData).then((response) => {
            if (response.code === 200) {
              this.$message.success('修改成功！')
              this.dialogForm.isShow = false
              this.loading()
            } else {
              this.$message.error('修改失败！')
            }
          })
        } else {
          console.log(this.dialogForm.formData);
          down(this.dialogForm.formData).then(
            response => {
              if (response.code === 200) {
                this.$message.success('下载成功！')
                this.dialogForm.isShow = false
                this.loading()
              } else {
                this.$message.error('下载失败！')
              }
            }
          )
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
        getContractsLst({
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
        this.getCustomer()
        this.getStaff()
        this.getProject()
        this.getContracts()
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
      download(id) {
        console.log(this.dialogForm.contractsLst[id - 1]);
        down(this.dialogForm.contractsLst[id - 1]).then((response) => {
          if (response.code === 200) {
            this.$message.success('下载成功！')
            this.dialogForm.isShow = false
            this.loading()
          } else {
            this.$message.error('下载失败！')
          }
        })
      }
    },
    created() {
      this.loading()
    }
  }
</script>
