<template>
  <div class="table-container">
    <el-table
      :data="propData ? propData : tableData"
      width="100%"
      :row-class-name="rowClassName"
      :height="height"
      :row-style="{height: `${rowHeight}px`}">
      <template v-for="(item, index) in theadData">
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
      <el-table-column
        v-if="isShowControl && controlList.length > 0"
        :fixed="controlFixed"
        :label="controlLabel"
        align="center"
      >
        <template slot-scope="scope">
          <template v-for="item in controlList">
            <el-button
              v-if="!item.slot"
              :key="item.type"
              :title="item.title"
              :class="item.className ? item.className : ''"
              @click="doAction(scope.row, item.type)"
            >
              {{ item.title }}
            </el-button>
            <template v-else slot-scope="scope">
              <slot :name="item.type" :row="scope.row"></slot>
            </template>
          </template>
        </template>
      </el-table-column>
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
      default: () => []
    },
    theadData: { // 表格头标题
      type: Array,
      default: () => []
    },
    height: { // 表格高度
      type: [Number, String],
      default: 'calc(100% - 100px)'
    },
    rowHeight: { // 表格行高
      type: [Number, String],
      default: 44
    },
    isShowControl: { // 是否展示操作列
      type: Boolean,
      default: true
    },
    controlList: { // 操作栏操作按钮
      type: Array,
      default: () => []
    },
    controlFixed: { // 操作栏是否固定
      type: [String, Boolean],
      default: false
    },
    controlLabel: { // 操作栏列名
      type: String,
      default: '操作'
    },
    isShowPagination: { // 是否展示分页
      type: Boolean,
      default: true
    },
    total: { // 表格总数
      type: Number,
      default: 0
    },
    currentPageName: { // 当前页码名称
      type: String,
      default: 'currentPage'
    },
    pageSizeName: { // 每页条数名称
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
    doAction (row = {}, type = '') {
      this.$emit('handleDoAction', { row, type })
    },
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
  height: 100%;

  /deep/ .el-table {
    background-color: transparent;

    &::before { // 表格底部边框
      background: none;
    }

    tbody tr:hover > td { // 表格触碰样式
      background-color: #F5F7FA;
    }

    .el-table__header-wrapper, el-table__fixed-header-wrapper {
      .el-table__cell { // 表头样式
        height: 44px;
        padding: 0;
        background: #FFFFFF;
        border-bottom: #EBEEF5 solid 1px !important;
        text-align: center;
      }
    }

    .el-table__body-wrapper, .el-table__fixed-body-wrapper {
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
}
</style>
