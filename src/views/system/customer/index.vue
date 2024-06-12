<template>
  <div class="manage">
    <el-dialog :title="dialogForm.type === 'add' ? '新增客户' : '更新客户'" :visible.sync="dialogForm.isShow">
      <el-form ref="form" label-width="100px" :model="dialogForm.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="客户名称" style="display:inline-block;width:300px" prop="name">
            <el-input placeholder="请输入名称" v-model.trim="dialogForm.formData.cname" />
          </el-form-item>
          <el-form-item label="客户电话" style="display:inline-block;width:300px" prop="c_phone">
            <el-input placeholder="请输入电话" v-model.trim="dialogForm.formData.cphone" />
          </el-form-item>
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="客户类型" style="display:inline-block" prop="ccompanyType">
            <el-select placeholder="请选择类型" v-model="dialogForm.formData.ccompanyType">
              <el-option value="有限责任公司" />
              <el-option value="股份有限公司" />
              <el-option value="国有独资责任公司" />
              <el-option value="私营企业" />
              <el-option value="国营企业" />
              <el-option value="外资企业" />
              <el-option value="合资企业" />
              <el-option value="民营企业" />
            </el-select>
          </el-form-item>
          <el-form-item label="客户地址" style="display:inline-block;width:300px" prop="caddress">
            <el-input placeholder="请输入企业地址" v-model.trim="dialogForm.formData.caddress" />
          </el-form-item>
        </el-form-item>
        <el-form-item label="客户来源" label-width="140px" style="width: 340px" prop="csource">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.csource" />
        </el-form-item>

        <el-form-item label="客户行业" label-width="140px" style="width: 450px" prop="cindustry">
          <el-input placeholder="请输入" v-model.trim="dialogForm.formData.cindustry" />
        </el-form-item>
        <el-form-item label-width="40px" style="margin-bottom:4px ">
          <el-form-item label="创建时间" style="display:inline-block" prop="cCreateTime">
            <el-date-picker type="date" value-format="yyyy-MM-dd" placeholder="请选择创建时间"
              v-model="dialogForm.formData.cCreateTime" />
          </el-form-item>
          <el-form-item label="重要程度" style="display:inline-block" prop="cimportance">
            <el-select placeholder="请选择类型" v-model="dialogForm.formData.cimportance">
              <el-option value="一般" />
              <el-option value="重要" />
            </el-select>
          </el-form-item>
          <el-form-item label="上级公司"  style="display:inline-block" prop="csuperiorCompany">
            <el-input placeholder="请输入" v-model.trim="dialogForm.formData.csuperiorCompany" />
          </el-form-item>
        </el-form-item>
        <el-form-item label="客户简介" label-width="140px" style="width:450px" prop="ccomment">
          <el-input type="textarea" placeholder="请输入" v-model.trim="dialogForm.formData.ccomment"
            :autosize="{ minRows: 4, maxRows: 6}" maxlength="1000" show-word-limit />
        </el-form-item>
      </el-form>

      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogForm.isShow = false">取消</el-button>
        <el-button type="primary" @click="confirm">确定</el-button>
      </div>
    </el-dialog>

    <!-- 点击联系人后 -->
    <el-dialog title="联系人" :visible.sync="customerDialog.isShow">
      <el-form ref="form" label-width="100px" :model="customerDialog.contactDetail" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px">
          <el-form-item label="联系人姓名" style="display:inline-block;width:300px" prop="ccName">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccName" contenteditable="false" />
          </el-form-item>
          <el-form-item label="性别" style="display:inline-block;width:300px" prop="ccSex">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccSex" contenteditable="false" />
          </el-form-item>
          <el-form-item label="年龄" style="display:inline-block;width:300px" prop="ccAge">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccAge" contenteditable="false" />
          </el-form-item>
          <el-form-item label="职位" style="display:inline-block;width:300px" prop="ccPosition">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccPosition" contenteditable="false" />
          </el-form-item>
          <el-form-item label="手机号" style="display:inline-block;width:300px" prop="ccPhone">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccPhone" contenteditable="false" />
          </el-form-item>
          <el-form-item label="邮箱" style="display:inline-block;width:300px" prop="ccEmail">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccEmail" contenteditable="false" />
          </el-form-item>
          <el-form-item label="负责工作" style="display:inline-block;width:300px" prop="ccJobs">
            <el-input placeholder="" v-model.trim="customerDialog.contactDetail.ccJobs" contenteditable="false" />
          </el-form-item>
          <el-form-item label="重点需求" style="display:inline-block;width:500px" prop="ccCareabout">
            <el-input type="textarea" :rows="4" placeholder="" v-model.trim="customerDialog.contactDetail.ccCareabout"
              contenteditable="false" />
          </el-form-item>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="customerDialog.isShow = false">取消</el-button>
        <el-button type="primary" @click="customerDialog.isShow = false">确定</el-button>
      </div>
    </el-dialog>

    <!-- 点击联系人后没有数据后选择添加 -->
    <el-dialog title="联系人" :visible.sync="customerContactDialog.isShow">
      <el-form ref="form" label-width="100px" :model="customerContactDialog.formData" size="mini">
        <el-form-item label-width="40px" style="margin-bottom:4px">
          <el-form-item label="联系人姓名" style="display:inline-block;width:300px" prop="ccName">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccName" contenteditable="false" />
          </el-form-item>
          <el-form-item label="性别" style="display:inline-block;width:300px" prop="ccSex">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccSex" contenteditable="false" />
          </el-form-item>
          <el-form-item label="年龄" style="display:inline-block;width:300px" prop="ccAge">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccAge" contenteditable="false" />
          </el-form-item>
          <el-form-item label="职位" style="display:inline-block;width:300px" prop="ccPosition">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccPosition" contenteditable="false" />
          </el-form-item>
          <el-form-item label="手机号" style="display:inline-block;width:300px" prop="ccPhone">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccPhone" contenteditable="false" />
          </el-form-item>
          <el-form-item label="邮箱" style="display:inline-block;width:300px" prop="ccEmail">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccEmail" contenteditable="false" />
          </el-form-item>
          <el-form-item label="负责工作" style="display:inline-block;width:300px" prop="ccJobs">
            <el-input placeholder="" v-model.trim="customerContactDialog.formData.ccJobs" contenteditable="false" />
          </el-form-item>
          <el-form-item label="重点需求" style="display:inline-block;width:500px" prop="ccCareabout">
            <el-input type="textarea" :rows="4" placeholder="" v-model.trim="customerContactDialog.formData.ccCareabout"
              contenteditable="false" />
          </el-form-item>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="customerDialog.isShow = false">取消</el-button>
        <el-button type="primary" @click="confirmCC()">确定</el-button>
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
        <el-form-item label="客户名称" prop="cname">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.cname" prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="上级公司" prop="csuperiorCompany">
          <el-input placeholder="请输入" v-model.trim="searchForm.formData.csuperiorCompany"
            prefix-icon="el-icon-search" />
        </el-form-item>
        <el-form-item label="客户类型" style="display:inline-block" prop="ccompanyType">
          <el-select placeholder="请选择类型" v-model="searchForm.formData.ccompanyType">
            <el-option value="有限责任公司" />
            <el-option value="股份有限公司" />
            <el-option value="国有独资责任公司" />
            <el-option value="私营企业" />
            <el-option value="国营企业" />
            <el-option value="外资企业" />
            <el-option value="合资企业" />
            <el-option value="民营企业" />
          </el-select>
        </el-form-item>
        <el-form-item label="关注度" prop="cimportance">
          <el-select placeholder="请选择" v-model="searchForm.formData.cimportance">
            <el-option label="一般" value="一般" />
            <el-option label="重要" value="重要" />
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
        <el-table-column prop="cid" label="客户ID" min-width="80" align="center" />
        <el-table-column prop="cname" label="客户名称" min-width="280" align="center" />
        <el-table-column prop="ccompanyType" label="企业性质" min-width="80" align="center" />
        <el-table-column prop="caddress" label="企业地址" min-width="225" align="center" />
        <el-table-column prop="csource" label="客户来源" min-width="100" align="center" />
        <el-table-column prop="cindustry" label="行业" min-width="125" align="center" />
        <el-table-column prop="cCreateTime" label="创建时间" min-width="125" align="center" />
        <el-table-column prop="cimportance" label="重要程度" min-width="125" align="center" />
        <el-table-column prop="csuperiorCompany" label="上级公司" min-width="200" align="center" />
        <el-table-column prop="cupdatePerson" label="创建人" min-width="100" align="center" />
        <el-table-column label="操作" width="280" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" @click="handleEdit(scope.row)">编辑 <i class="el-icon-edit"></i>
            </el-button>
            <el-popconfirm style="margin-left:10px;margin-right:10px" confirm-button-text='确定' cancel-button-text='我再想想'
              icon="el-icon-info" icon-color="red" title="你确定删除吗？" @confirm="handleDelete(scope.row.cid)">
              <el-button size="mini" type="danger" slot="reference">删除 <i class="el-icon-remove-outline"></i>
              </el-button>
            </el-popconfirm>
            <el-button type="warning" @click="getCustomerDetail(scope.row.cid)">联系人 <i class="el-icon-user-solid" />
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
    getCustomerList,
    getOne,
    add,
    getExportApi,
    getImportApi,
    edit
  } from '../../../api/customer'

  import {
    getCustomerContactList,
    getOneCustomerContact,
    addCC
  } from '../../../api/customer-contact.js'

  import {
    getContractsList
  } from '../../../api/contracts'
  import {
    getAllDept
  } from '../../../api/dept'
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
          ccompanyTypeList: [],
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
        customerId: 0
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

      // 点击新增按钮，弹出对话框
      handleAdd() {
        this.dialogForm.isShow = true
        this.dialogForm.type = 'add'
        this.dialogForm.formData = {}
        this.getDept()
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
      // 加载所有部门数据
      loading() {
        getCustomerList({
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
        getCustomerContactList().then(response => {
          if (response.code === 200) {
            this.table.tableDataContact = response.data.list
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
      confirmCC(){
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
      getCustomerDetail(id) {
        this.customerId = id
        getOneCustomerContact(this.customerId).then(response => {
          if (response.code === 200) {
            this.customerDialog.isShow = true
            this.customerDialog.contactDetail = response.data
            console.log(this.customerDialog.contactDetail);
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
