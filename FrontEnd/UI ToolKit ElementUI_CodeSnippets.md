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

```html
<el-cascader ref="cascader" :props="cascaderProps" :options="options" v-model="target">
	<template slot-scope="{ node, data }">
		<div @click="nodeClick(data, target)">
			<span>{{ data.label }}</span>
		</div>
	</template>
</el-cascader>

<script>
	export default {
		data() {
			return {
				target: '', // 与数据中的 value 字段类型对应
				cascaderProps: {
					checkStrictly: true,
					expandTrigger: 'hover',
					emitPath: false,
				},
				options: [
					{
						label: '广东',
						value: '440000',
						children: [
							{ label: '广州', value: '440100' },
							{ label: '深圳', value: '440300' },
						],
					},
					{
						label: '宁夏',
						value: '640000',
						children: [{ label: '银川', value: '640100' }],
					},
				],
			};
		},
		methods: {
			nodeClick(nodeData, target) {
				target = nodeData.value;
				this.$refs.cascader.checkedValue = nodeData.value;
				this.$refs.cascader.computePresentText();
				this.$refs.cascader.toggleDropDownVisible(false);
				this.$message({
					message: '已选择：' + nodeData.label,
					type: 'success',
					duration: 1000,
				});
			},
		},
	};
</script>

<style lang="scss" scoped>
	.DepartmentSelector {
		.el-cascader {
			width: 100% !important;
			& > div {
				width: 100% !important;
			}
		}
		& >>> .el-cascader-node__label * {
			user-select: none;
		}
	}
</style>
```

-   表单内只含有一个表单项，回车事件触发的表单提交

```html
<el-form :model="query" @submit.native.prevent>
	<el-form-item>
		<el-input v-model="query.positionName" @keyup.enter.native="toQuery" />
	</el-form-item>
</el-form>
```

-   Element UI 组件库修改组件 props 原型链上的默认值

```javascript
Element.Form.props.validateOnRuleChange.default = false;
```
