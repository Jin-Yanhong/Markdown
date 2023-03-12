## 表格

-   添加状态切换开关

```html
<el-table-column label="状态" align="center">
	<template slot-scope="scope">
		<el-switch v-model="scope.row.state" :active-value="'true'" :inactive-value="'false'" @change="handleStatusChange(scope.row)"></el-switch>
	</template>
</el-table-column>
```

-   数据字典调用

```html
<el-table-column label="公司状态" align="center">
	<template slot-scope="scope">
		<el-tag :type="">{{ }}</el-tag>
	</template>
</el-table-column>
```

-   表格序号

```html
<el-table-column label="序号" align="center">
	<template slot-scope="scope">
		<span>{{ pageSize * pageNum + scope.$index + 1 }}</span>
	</template>
</el-table-column>
```
