<template>
   <div>
    <el-card class="box-card">
			<div class="mod-dept">
				<el-form :inline="true" :model="selectDept" class="demo-form-inline">
					<el-form-item>
						<el-input v-model="selectDept.name" clearable placeholder="请输入用户名称" @clear='getDataList'></el-input>
					</el-form-item>
					<el-form-item>
						<el-button type="primary" @click="getDataList">查询</el-button>
						<!-- <el-button type="primary">增加</el-button> -->
					</el-form-item>
				</el-form>

				<el-table :data="dataList" border style="width: 100%">
					<el-table-column type="selection"> </el-table-column>
					<el-table-column prop="id" label="ID" width="60">
					</el-table-column>
					<el-table-column prop="name" label="用户名称" width="120">
					</el-table-column>
					<el-table-column prop="operation" label="操作" width="120">
					</el-table-column>
					<el-table-column prop="method" label="请求方法" width="430">
					</el-table-column>
					<el-table-column prop="params" label="请求参数" width="120">
					</el-table-column>
                    <el-table-column prop="time" label="执行时长(毫秒)" width="120">
					</el-table-column>
					<el-table-column prop="createDate" label="创建时间" width="200">
						<template slot-scope="scope">
						<span>{{ scope.row.createDate == null ? '' : scope.row.createDate.replace("T", " ") }}</span>
					</template>
					</el-table-column>
				</el-table>
				<el-pagination @size-change="sizeChangeHandle" @current-change="currentChangeHandle"
					:current-page="pageIndex" :page-sizes="[5,7, 10]" :page-size="pageSize" :total="totalPage"
					layout="total, sizes, prev, pager, next, jumper" style="margin-top: 30px">
				</el-pagination>
			</div>
		</el-card>
</div>
</template>

<script>

export default {
   data(){
    return{
      selectDept: {name: null},
			dataList: [], //数据列表
			pageIndex: 1,   //初始页
			pageSize: 5,        //每页条数
			totalPage: 0,         //总条数
			dataListLoading: false,
    }
   },
   methods:{
		//每页显示几条
		sizeChangeHandle(val) {
			this.pageSize = val;
			this.pageIndex = 1;
			this.getDataList()
		},
		//当前页
		currentChangeHandle(val) {
			this.pageIndex = val;
			this.getDataList()
		},
        		//获取初始化数据
		getDataList() {
			if (this.dataListLoading) {
				return;
			}
			// this.dataListLoading=true;
			//请求参数封装
			const params = {
				params: {
					pageSize: this.pageSize,
					pageNum: this.pageIndex,
					keyword: this.selectDept.name
				}
			};

      console.log(this.selectDept);
			//后端请求 分页获取对象
			this.$http.get("log/list", params).then((res) => {
				// console.log("提交的参数", params);
				  console.log(res);
				//需要通过响应的结果配置
				this.dataList = res.data.data.list;
				this.totalPage = res.data.data.total;
				this.dataListLoading = false;

			});
		},
   },
   mounted(){
	this.getDataList()
   }
}
</script>
<style lang='less' scoped>

</style>
