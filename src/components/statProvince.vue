<template>
  <div class="main">
    <div class="filter-box">
      <v-input :formData="filterForm" :opt="channel"></v-input>
      <br>
      <v-input :formData="filterForm" :opt="client"></v-input>
      <br>
      <date-picker :formData="filterForm"  type="date" :opt="dataRange" dateFormat="yyyy-MM-dd"></date-picker>
      <div class="btn-right-wrap">
        <el-button size="small" type="primary" @click="search" :loading="isLoading">筛选</el-button>
      </div>
    </div>

    <el-row :gutter="20" class="table-header">
      <el-col :span="2" :offset="20">&nbsp;<!--<el-button size="small"><i class="iconfont icon-download"></i>下载</el-button>--></el-col>
      <!--<el-col :span="2" ><el-button icon="plus" size="small" @click="modifyType=1;dialogUserModifyVisible=true">新建</el-button></el-col>-->
    </el-row>

    <el-table
        v-loading="isLoading"
        :data="tableData"
        stripe
        :row-class-name="tableRowClassName">
      <!-- <el-table-column
           type="index"
           width="50">
       </el-table-column>-->
      <!--<el-table-column
          fixed
          prop="date"
          width="120"
          label="日期">
      </el-table-column>
      <el-table-column
          prop="op_id"
          label="通道ID">
      </el-table-column>-->

      <el-table-column
          v-for="(item, idx) in columns" :key="idx"
          :prop="item"
          :label="item">
      </el-table-column>

      <!-- <el-table-column
           fixed="right"
           label="操作"
           width="100px">
         <template scope="scope">
           &lt;!&ndash;<el-button @click="onDetail" type="text" size="small">查看</el-button>&ndash;&gt;
           <el-button @click.prevent="onEdit(scope.$index, scope.row)" type="text" size="small">编辑</el-button>
           &lt;!&ndash;<el-button @click.prevent="onDelete" type="text" size="small">删除</el-button>&ndash;&gt;
         </template>
       </el-table-column>-->
    </el-table>

    <div class="mt15">
      <!--<el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-size="pageSize"
          layout="total, prev, pager, next, jumper"
          :total="total">
      </el-pagination>-->
    </div>

  </div>
</template>

<script>
  import vInput from './filters/vInput'
  import datePicker from './filters/datePicker'
  import _base from '../mixin/base.js'
  import _pagination from '../mixin/pagination.js'
  import moment from 'moment'

  import Services from 'common/js/services.js'

  const dateFormat = 'YYYY-MM-DD'

  export default {
    mixins: [_base, _pagination],
    name: 'channelDelay',
    data () {
      return {
        channel: {
          name: '通道',
          key: 'op_id',
          placeHolder: '请输入通道id'
        },
        client: {
          name: '客户',
          key: 'sp_id',
          placeHolder: '请输入客户账号'
        },
        dataRange: {
          name: '起止时间',
          keyStart: 'start_time',
          keyEnd: 'end_time',
          desc: '可查询三个月内记录'
        },
        filterForm: {
          op_id: '',
          sp_id: '',
          start_time: moment().subtract(7, 'days').format(dateFormat),
          end_time: moment().subtract(1, 'days').format(dateFormat)
        },
        columns: [],
        tableData: []
      }
    },
    watch: {
      currentPage () {
        this.getList()
      }
    },
    created () {
      this.getList()
    },
    methods: {
      search () {
        this.getList()
      },
      getList (page) {
        let params = Object.assign({}, this.filterForm)
        params['start_time'] = moment(params['start_time']).format(dateFormat)
        params['end_time'] = moment(params['end_time']).format(dateFormat)
        params['page'] = this.currentPage
        this.requestPost(Services.province2, params, (remoteData) => {
          // this.columns = remoteData.list_title
          this.tableData = this.formatTableData(remoteData)
          this.pageSize = remoteData.page_size
          this.total = parseInt(remoteData.total)
        })
      },
      formatTableData (data) {
        let rData = []
        let columns = data.abscissa || []
        let rows = data.ordinate
        let rowsData = data.ordinate_data
        columns.unshift('延迟时间')
        this.columns = columns
        rows.forEach((key, idx) => {
          let row = rowsData[key]
          row['延迟时间'] = key
          rData.push(row)
        })
        return rData
      },
      tableRowClassName (row, index) {
        return ''
      }
    },
    components: {
      vInput, datePicker
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
  .user-dialog
    .el-input__inner
      width: 200px

</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
