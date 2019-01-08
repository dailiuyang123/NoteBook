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
