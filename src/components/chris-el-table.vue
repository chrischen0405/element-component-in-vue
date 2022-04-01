<template>
    <div class="table-container">
        <el-table
                :data="tableData"
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
    </div>
</template>

<script>
export default {
    name: 'chris-el-table',
    props: {
        tableData: { // 表格数据
            type: Array,
            default: () => {
                return []
            }
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
        }
    },
    data () {
        return {}
    },
    methods: {
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
