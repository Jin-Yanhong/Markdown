## 表格

-   添加状态切换开关

```vue
<el-table-column label="状态" align="center">
    <template slot-scope="scope">
        <el-switch
            v-model="scope.row.state"
            :active-value="'true'"
            :inactive-value="'false'"
            @change="handleStatusChange(scope.row)"
        ></el-switch>
    </template>
</el-table-column>
```

-   数据字典调用

```vue
<el-table-column label="公司状态" align="center">
    <template slot-scope="scope">
        <el-tag :type="companyOptions[parseInt(scope.row.status)].listClass">
            {{ companyOptions[parseInt(scope.row.status)].dictLabel }}
        </el-tag>
    </template>
</el-table-column>
```

​
