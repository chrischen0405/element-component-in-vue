<template>
  <div class="home">
    <chris-form-item
      :form-items="theadData"
      :query="query"
      @reload="reload"
    ></chris-form-item>
    <chris-el-table
      :thead-data="theadData"
      :prop-data="tableData"
      :control-list="controlList"
      :is-show-pagination="true"
      :total="tableData.length"
      current-page-name="page"
      page-size-name="rows"
      @onPageChange="onPageChange"
      @handleDoAction="handleDoAction"
    >
      <el-table-column slot="handle" label="查看">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)">查看</el-button>
        </template>
      </el-table-column>
    </chris-el-table>
  </div>
</template>

<script>
import ChrisElTable from '../../components/ChrisElTable/index'
import {
  controlList,
  theadData
} from './table-config'
import ChrisFormItem from '../../components/ChrisFormItem/index'

export default {
  name: 'Home',
  components: {
    ChrisFormItem,
    ChrisElTable
  },
  data () {
    return {
      theadData,
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
      ],
      controlList,
      query: {}
    }
  },
  created () {
    this.setQuery()
  },
  methods: {
    setQuery (query = {}) {
      this.theadData
        .filter(e => e.search)
        .forEach(opt => {
          const { property } = opt
          this.query[property] = query[property] || ''
        })
      this.query = { ...this.query }
    },
    handleClick (item) {
      console.log(item)
    },
    handleDoAction (e) {
      console.log(e)
    },
    onPageChange (ev) {
      console.log(ev)
    },
    reload (query, type) {
      if (type === 'search') {
        console.log(query)
        this.setQuery(query)
      }
    }
  }
}
</script>
