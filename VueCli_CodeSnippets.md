- 路由传参
  
- 传递参数

  ```javascript
  this.$router.push({
      name: '',//此处的 name 是路由 路径下的 name 属性
      params: {
          page: '1', code: '8989'
    }
    })
  ```

- 接收参数

- ```javascript
  this.page = this.$route.params.page// 用$route接收，少个r,注意啦
  ```

- npm i --save animate.css@3

  element-ui表格添加序号列

  ```
  <el-table-column label="序号" align="center">
      <template slot-scope="scope">
          <span>
              {{ pageSize * pageNum + scope.$index + 1 }}
          </span>
      </template>
  </el-table-column>
  ```

- 函数方法的执行要略微晚于DOM的加载，写在DOM里的方法可以用箭头函数执行
