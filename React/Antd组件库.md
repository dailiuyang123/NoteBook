#Antd 阿里组件库


* 时间选择框 收参/回显
````javascript
        import Datapicker from ant

           <FormItem
              {...formItemLayout}
              label="有效期结束时间"
            >
              {getFieldDecorator('endDate',{
                initialValue:moment((tempRecord === null ? "":tempRecord.endDate),'YYYY-MM-DD')
              })(
                <DatePicker  style={{ width: '300px' }} format="YYYY-MM-DD" placeholder="请选择" />
              )}
            </FormItem>

````

* 下拉列表 收参/回显
```javascript
 <FormItem
              {...formItemLayout}
              label="适用组织"
            >
              {getFieldDecorator('ruleClassifyId', {
                initialValue : (tempRecord === null ? "":tempRecord.ruleClassifyId),
                rules: [{
                  required: true, message: '请选择适用组织!',
                }],
              })(
                <Select
                  showSearch={true}
                  filterOption={false}
                  placeholder="请选择"
                  onSearch={this.fetchUserRole}
                  // onChange={this.handleChange}
                  style={{ width: '300px' }}
                >
                  {this.state.effectiveBuInfo.map(d => <Option key={d.id} value={d.dept_id}>{d.bu_name}</Option>)}
                </Select>
              )}
            </FormItem>

```

* 级联下拉列表回显
```javascript
//收参
let vals = this.props.form.getFieldsValue();
//获取日期
vals.endDate=vals.endDate['_d'];


      <FormItem
              {...formItemLayout}
              label="考核类型与考核周期"
            >
              {getFieldDecorator('checkPeriodAndType', {
                initialValue :(tempRecord === null ? "":tempRecord.checkPeriodAndType),
                rules: [{
                  required: true, message: '请选择考核类型与考核周期',
                }],
              })(
                <Cascader style={{width:'300px'}} options={options} onChange={onChange} placeholder="please select" />
              )}
            </FormItem>

```
* 实时获取 input 输入框内输入的值
```javascript
// DOM 节点
 <Input placeholder=""  maxLength={50} style={{width:'300px'}} onChange={(val)=>this.getRuleCname(val)} />

// 获取规则名称 event.target.value获取输入的值
  getRuleCname(event){
    //alert(event.target.value)
    if (event.target.value!==''&& event.target.value!==undefined){
      this.setState({initTag:event.target.value});
    }else {
      this.setState({initTag:'计算公式'});
    }

  }
```

* ant Table 组件
```javascript
   code： <Table dataSource={list} columns={colums} loading={loading} pagination={pagination} scroll={{x: 1800}}
                        rowKey={record => record.userCode}/>
                        
      datasource: table 数据源
      columns：table 包含的列
      pagination： table 的组件配置（如分页组件）， 如果置为false 则为取消分页效果
      scroll： 设置table的滚动条
      rowKey:设置表内记录的唯一标识。一般为 记录ID                  
                        
```


