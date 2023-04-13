<template>
  <div class="table-container">
    <el-table
      :data="propData ? propData : tableData"
      width="100%"
      :row-class-name="rowClassName"
      :height="height"
      :row-style="{height: `${rowHeight}px`}">
      <template v-for="(item, index) in tableTitle">
        <slot v-if="item.slot" :name="item.slot"></slot>
        <el-table-column
          v-else
          :key="index"
          :prop="item.property"
          :label="item.label"
          :min-width="item.minWidth ? item.minWidth : ''"
          :width="item.width ? item.width : ''">
        </el-table-column>
      </template>
    </el-table>
    <chris-el-pagination
      v-if="isShowPagination"
      :current-page="currentPage"
      :page-size="pageSize"
      :total="total ? total : totalNum"
      :current-page-name="currentPageName"
      :page-size-name="pageSizeName"
      @onChange="onPageChange"
    ></chris-el-pagination>
  </div>
</template>

<script>
import ChrisElPagination from '../ChrisElPagination/index'

export default {
  name: 'ChrisElTable',
  components: {
    ChrisElPagination
  },
  props: {
    propData: { // 表格数据
      type: Array,
      default: null
    },
    tableTitle: { // 表格头标题
      type: Array,
      require: true
    },
    height: { // 表格高度
      type: [Number, String],
      default: '100%'
    },
    rowHeight: { // 表格行高
      type: [Number, String],
      default: 44
    },
    isShowPagination: {
      type: Boolean,
      default: true
    },
    total: {
      type: Number,
      default: 0
    },
    currentPageName: {
      type: String,
      default: 'currentPage'
    },
    pageSizeName: {
      type: String,
      default: 'pageSize'
    }
  },
  data () {
    return {
      tableData: [],
      currentPage: 1,
      pageSize: 10,
      totalNum: 0
    }
  },
  methods: {
    onPageChange (ev) {
      console.log(ev)
      this.currentPage = ev[this.currentPageName]
      this.pageSize = ev[this.pageSizeName]
      this.$emit('onPageChange', ev)
    },
    rowClassName (e) {
      return e.rowIndex % 2 === 0 ? '' : 'light-line'
    }
  }
}
</script>

<style scoped lang="scss">
.table-container {
  /deep/ .el-table {
    background-color: transparent;

    &::before { // 表格底部边框
      background: none;
    }

    tbody tr:hover > td { // 表格触碰样式
      background-color: #F5F7FA;
    }
  }

  /deep/ .el-table__header-wrapper {
    .el-table__cell { // 表头样式
      height: 44px;
      padding: 0;
      background: #FFFFFF;
      border-bottom: #EBEEF5 solid 1px !important;
      text-align: center;
    }
  }

  /deep/ .el-table__body-wrapper {
    &::-webkit-scrollbar { // 表格滚动条
      width: 0 !important;
    }

    .el-table__row { // 表格行样式
      background-color: #F5F7FA;

      .el-table__cell {
        padding: 0;
        text-align: center;
        border-bottom: #EBEEF5 solid 1px !important;
      }
    }

    .light-line { // 高亮行颜色
      background-color: #FFFFFF;
    }
  }
}
</style>
