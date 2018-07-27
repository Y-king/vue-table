<template>
    <div class="pagination">
        <el-pagination
            background
            @current-change="handleCurrentChange"
            :current-page="currentPage"
            :page-sizes="[5, 10, 15, 30]"
            :page-size="pageSize"
            layout="total, prev, pager, next"
            :total="total">
        </el-pagination>
    </div>
</template>
<script>
let curPage = 1;
export default {
    props: {
        total: {
            type: Number,
            default: 0
        },
        currentPage: {
            type: Number,
            default: 1
        }
    },
    data() {
        return {
            pageSize: 15
        };
    },
    methods: {
        handleCurrentChange(val) {
            this.curPage = val;
            this.$emit('pageChange',val);
        }
    }
};
</script>

<style scoped>
    .el-pagination{margin-top: 10px; margin-bottom: 10px;}
</style>
