<template>
  <div class="home">
    <chris-el-table
      :table-title="tableTitle"
      :prop-data="tableData"
      :is-show-pagination="true"
      :total="tableData.length"
      current-page-name="page"
      page-size-name="rows"
      @onPageChange="onPageChange"
    >
      <el-table-column slot="handle" label="操作">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)">查看</el-button>
        </template>
      </el-table-column>
    </chris-el-table>
  </div>
</template>

<script>
import ChrisElTable from '../../components/ChrisElTable/index'
import { tableTitle } from './table-config'

export default {
  name: 'Home',
  components: {
    ChrisElTable
  },
  data () {
    return {
      tableTitle,
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }
      ]
    }
  },
  methods: {
    handleClick (item) {
      console.log(item)
    },
    onPageChange (ev) {
      console.log(ev)
    }
  }
}
</script>
