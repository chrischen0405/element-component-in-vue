<template>
  <div class="pagination-container">
    <el-pagination
      v-bind="$attrs"
      :current-page="currentPage"
      :page-size="pageSize"
      :total="total"
      :page-sizes="pageSizes"
      background
      :layout="layout"
      @size-change="sizeChange"
      @current-change="currentChange"
    ></el-pagination>
  </div>
</template>

<script>
export default {
  name: 'ChrisElPagination',
  props: {
    currentPage: {
      type: Number,
      default: 1
    },
    pageSize: {
      type: Number,
      default: 10
    },
    total: {
      type: Number,
      default: 0
    },
    pageSizes: {
      type: Array,
      default: () => {
        return [10, 20, 30, 40, 50, 100]
      }
    },
    layout: {
      type: String,
      default: 'prev, pager, next, jumper, sizes'
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
  methods: {
    sizeChange (pageSize) {
      this.$emit('onChange', {
        [this.currentPageName]: 1,
        [this.pageSizeName]: pageSize
      })
    },
    currentChange (currentPage) {
      this.$emit('onChange', {
        [this.currentPageName]: currentPage,
        [this.pageSizeName]: this.pageSize
      })
    }
  }
}
</script>

<style scoped lang="scss">
.pagination-container {
  text-align: right;
}
</style>
