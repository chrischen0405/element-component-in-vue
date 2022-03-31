<template>
    <div class="home">
        <chris-el-table
                :table-title="tableTitle"
                :table-data="tableData">
            <el-table-column slot="handle" label="操作">
                <template slot-scope="scope">
                    <el-button @click="handleClick(scope.row)">查看</el-button>
                </template>
            </el-table-column>
        </chris-el-table>
    </div>
</template>

<script>
import ChrisElTable from '../components/chris-el-table'

export default {
    name: 'Home',
    components: { ChrisElTable },
    data () {
        return {
            tableTitle: [
                {
                    label: '日期',
                    property: 'date'
                },
                {
                    label: '姓名',
                    property: 'name'
                },
                {
                    label: '地址',
                    property: 'address'
                },
                {
                    slot: 'handle'
                }
            ],
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
        }
    }
}
</script>
