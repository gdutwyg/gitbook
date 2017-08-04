# elementUI使用心得
正式使用vue和elementUI已经刚刚一个月了，在这一个月中，使用vue和elementUI做了一个项目，下面就使用的过程中自己体会的，学习到的记录下来。

1. **resetFields(表单重置)** 描述：对整个表单进行重置，将所有字段值重置为 **初始值**并移除校验结果  所以请记住是初始值（有可能是有值的，也有可能是空值的）

2. vue-cli 的url中有#， 如果去掉？ 
  - 这个因为你使用了vue-router你只需去掉vue-router的使用
  - 或者在[vue-router](https://router.vuejs.org/zh-cn/)中设置`mode`为`history`即可

3. 当数据是请求回来的（有延时，异步），例如你一开始设置默认值为空字符串，但是请求回来是数组，你如果在数据绑定时使用了数组的方法，则会报错你（undefined），如何解决？
  - 添加一个v-if=“数据”，确保数据回来了再渲染，此时不会报错
4. 表格手动传输数据 
   ```html
  <template scope="scope">{{ scope.row.date }}</template>
   ```
   自动传输数据
   ```html
    <el-table-column prop="date" label="日期" width="180">
    </el-table-column>
   ```

5. elementUi 日期选择器支持传入时间戳或者时间对象（它会自动解析），不要传递字符串，**切记**


