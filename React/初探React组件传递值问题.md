# 初探 React 组件间值传递

##场景：数据列表页面+ 查看+新建 弹框页面

* CODE:
```javascript


const FormItem = Form.Item;
const Option = Select.Option;
const confirm = Modal.confirm;
const ProductGrouNames={"1":"全部产品","2":"新业务","3":"传统业务"};
const modelKey='PublishAmountModel/';
const downLoadExcelTpl = modelKey + 'downLoadExcelTpl';
const modelSetStateInfo = modelKey + 'setStateInfo';
const changeInfo=modelKey+'getChangeInfoDetail';
const delRecord=modelKey+'deleteChangeByid';
const editRecord=modelKey+'editChangeAmount';

     // 数据列表
    class PublishAmount extends React.Component{
    
     constructor(props){
        super(props);
        this.state={
          visible:false,
          totalCount:0,
          record:null
        }
        this.bind();
        this.operationData = getPageOperationList(props.pageOperationList, "/PublishAmount");
        let self = this;
        this.colums=[
          {title:"合同号",dataIndex:"csn",key:"csn"},
          {title:"产品线",dataIndex:"productGroupName",key:"productGroupName"},
          {title:"调整月份",dataIndex:"monthPeriod",key:"monthPeriod"},
          {title:"调整业务员",dataIndex:"userName",key:"userName"},
          {title:"调整金额(元)",dataIndex:"amount",key:"amount"},
          {title:"调整类型",dataIndex:"type",key:"type"},
          {title:"数据类型",dataIndex:"dataType",key:"dataType",render:function (text,record,index) {
            if(text==2){
              return '回款';
            }else {
              return '发布额';
            }
          }},
          {title:"流程状态",dataIndex:"flowState",key:"flowState",render:function (text,record,index) {
            if(text==='Enable'){
              return '生效';
            }else {
              return '失效'
            }
          }},
          {title:"日期",dataIndex:"createOn",key:"createOn",render:function (text,record,index) {
            return moment(record.createOn).format('YYYY-MM-DD HH:mm:SS');
          }},
          {
            title: "操作", dataIndex: "", key: "operation", width: 220, render: function (text, record, index) {
    
            let operArray = {
              "PublishAmount:see": <Link to="#" onClick={function () {self.showUpdateModal(record);}} replace>查看</Link>,
              "PublishAmount:del":<Link to="#" onClick={function () {self.deleteConfirm(record);}} replace>删除</Link>
            };
            self.operationArray = getOperationList(self.operationData,operArray);
            if (self.operationArray.length > 0){
              return <div>
                {
                  self.operationArray.map((item,index) => {
                    return item;
                  })
                }
              </div>
            }
          }
          }
        ]
    
      }
    
      bind(){
        this.search = this.search.bind(this);
        this.downLoadExcelTpl=this.downLoadExcelTpl.bind(this);
        this.exports=this.exports.bind(this);
        this.showUpdateModal=this.showUpdateModal.bind(this);
      }
    
    
      componentDidMount(){
        const {dispatch} = this.props;
        dispatch({type:'global/setBreadcrumbData',payload:["首页","业绩管理","业绩调整"]});
      }
    
      componentWillMount(){
        const {dispatch} = this.props;
        dispatch({type:'PublishAmountModel/getDataList',payload:{}});
        this.getEffectiveBuInfo()
      }
    
    
      componentWillUnmount(){
        const {dispatch} = this.props;
        dispatch({type:'PublishAmountModel/clearState',payload:{}});
      }
      getParams(vals){
        let params = {};
        params.userCode = vals.userCode;
        params.csn = vals.csn;
        params.type = vals.type;
        params.dataType=vals.dataType;
        return params;
      }
    
    
    
      // 弹窗方法
      showUpdateModal(record) {
        //初始化数据
        const {dispatch} = this.props;
        debugger
        if(record.id===undefined|| record.id===null){  //新建
          this.setState({
            visible: true,
            record:null
          });
        }else {                                        //查看
          new Promise(
            (resolve) => {
              dispatch({type:changeInfo,payload:{resolve,id:record.id}});
            }
          ).then((res) => {
              if (res != null) {
                if (res.code === 0) {
                  let tmpdata= res.data;
                  record.saleUser=tmpdata.saleUser;
                  record.publishMoney=tmpdata.publishMoney;
                  this.setState({
                    visible: true,
                    record:record
                  });
                }
                else {
                  message.error(res.msg);
                }
              }
              else {
                message.error("查询异常");
              }
            }
          ).catch ((res) => {
            message.error("查询异常");
          })
        }
    
    
      }
    
      //删除记录
      deleteConfirm(record){
        const {dispatch} = this.props;
        confirm({
          title: `确实要删除这条记录吗?`,
          okText: '确定',
          okType: 'danger',
          cancelText: '取消',
          onOk() {
            new Promise(
              (resolve) => {
                dispatch({type:delRecord,payload:{id:record.cid,resolve}});
              }
            ).then((res) => {
              debugger
              if(res.code === 0){
                message.success("删除成功！");
                dispatch({type:'PublishAmountModel/getDataList',payload:{}});
              }
              else{
                message.error("加载失败，请重试！");
              }
            });
          },
          onCancel() {
            console.log('Cancel');
          },
        });
    
    
    
      }
    
    
      handleOk(){
        setTimeout(() => {
          this.setState({
            visible: false,
            confirmLoading: false,
          });
        }, 2000);
      }
    
      handleCancel(){
        this.setState({
          visible: false,
        });
        this.formRef.props.form.resetFields();
      }
    
      // 确定更新按钮
      HandleUpdate() {
        const {dispatch} = this.props;
        debugger;
        const form = this.formRef.props.form;
        form.validateFields((err, fieldsValue) => {
          if (err) {
            return;
          }
          // 参数上传前预处理
          const values = {
            ...fieldsValue,
          };
          values.monthPeriod= values.monthPeriod.format('YYYYMM') ;
          values.productGroupName= ProductGrouNames[values.productGroupID];
          new Promise(
            (resolve) => {
              // 提交调整
              dispatch({type:editRecord,payload:{resolve,values}});
            }
          ).then((res) => {
            if (res != null) {
              if (res.code === 0) {
                this.setState({
                  visible: false,
                });
                message.success("保存成功");
                dispatch({type:'PublishAmountModel/setStateInfo',payload:{}});
                dispatch({type:'PublishAmountModel/getDataList',payload:{}});
              }
              else {
                message.error(res.msg);
              }
            }
            else {
              message.error("提交失败");
            }
          }).catch((res) => {
            message.error("提交失败");
          });
    
        });
      }
    
      saveFormRef(formRef) {
        this.formRef = formRef;
      }
    
      search(e){
        const {dispatch} = this.props;
        e.preventDefault();
        let vals = this.props.form.getFieldsValue();
        debugger
        let params = this.getParams(vals);
        dispatch({type:'PublishAmountModel/getDataList',payload:params});
      }
      getEffectiveBuInfo() {
        const {dispatch} = this.props;
        let vals = this.props.form.getFieldsValue();
        let param = this.getParams(vals);
    
      }
      exports(){
        const {dispatch} = this.props;
        let vals = this.props.form.getFieldsValue();
        let params = this.getParams(vals);
    
        new Promise(
          (resolve) => {
            dispatch({type:'PublishAmountModel/setStateInfo',payload:{resolve}});
            dispatch({type:'PublishAmountModel/getDataListExport',payload:{resolve,params}});
          }
        ).then((res) => {
          if (res.success === false){
            let hide = message.error(res.message);
            setTimeout(hide,1500);
          }
          else if (res.rows.length === 0 ){
            let hide = message.error("没有查询到记录！");
            setTimeout(hide,1500);
          }
          else {
            let data = res.rows;
            data.map(item=>item.dataDate=moment(item.dataDate).format('YYYY-MM-DD'))
            let titleMap = {};
            this.colums.map(function(obj){
              if (obj.dataIndex !== ""){
                titleMap[obj.dataIndex] = obj.title;
              }
            })
            downloadFile(data,titleMap,"业绩调整"+ moment(new Date()).format("YYYYMMDDHHmmSS"));
          }
        })
      }
    
      //模板下载
      downLoadExcelTpl() {
        const {dispatch} = this.props;
        dispatch({type: downLoadExcelTpl, payload: {template: "PublishAmountModel"}});
      }
    
      //导入
      showModal = () => {
        this.modal(true);
      }
    
      modal(visable) {
        const {dispatch} = this.props;
        dispatch({type: modelSetStateInfo, payload: {modalVisible: visable,}});
      }
    
      handleCancels = () => {
        this.modal(false);
      }
    
    
      handleFormReset = () => {
        const {form} = this.props;
        form.resetFields();
    
      };
    
        getFroms(){
            const {getFieldProps} = this.props.form;
            let countyName=(<FormItem label="姓名/工号">
              <Input  {...getFieldProps('userCode')}/>
            </FormItem>)
            let csn=(<FormItem label="合同号">
              <Input  {...getFieldProps('csn')}/>
            </FormItem>);
        
            let type=(<FormItem label="调整类型">
              <Select  {...getFieldProps('type')}>
                <Option value="全部">全部</Option>
                <Option value="增加">增加</Option>
                <Option value="减少">减少</Option>
              </Select>
            </FormItem>);
        
            let dataType=(<FormItem label="数据类型">
              <Select  {...getFieldProps('dataType')}>
                <Option value={0}>全部</Option>
                <Option value={1}>发布额</Option>
                <Option value={2}>回款</Option>
              </Select>
            </FormItem>);
            let forms = [];
            forms.push(countyName);
            forms.push(csn);
            forms.push(type);
            forms.push(dataType);
            return forms
          }
        
          render(){
            const {dispatch,list,total,pageIndex,loading,pageOperationList,totalCount} = this.props;
            if (pageOperationList === null || pageOperationList === undefined) {
              return;
            }
            let operationArray = [];
            if (this.operationData !== undefined  ) {
              if(this.operationData.containKey("PublishAmountModel:download")){
                operationArray.push(
                  <Button icon="cloud-download" type="primary" onClick={this.downLoadExcelTpl}>
                    下载模板
                  </Button>)
              }
        
              if(this.operationData.containKey("PublishAmountModel:import")){
                operationArray.push(
                  <Button icon="cloud-upload-o" type="primary" onClick={this.showModal}>
                    导入
                  </Button>)
              }
        
              if(this.operationData.containKey("PublishAmountModel:export")){
                operationArray.push(
                  <Button icon="export" htmlType="submit" type="primary" onClick={this.exports}>
                    导出
                  </Button>)
              }
        
              if(this.operationData.containKey("PublishAmountModel:add")){
                operationArray.push(
                  <Button icon="plus" htmlType="submit" type="primary" onClick={this.showUpdateModal}>
                    新建
                  </Button>)
              }
        
            }
            let vals = this.props.form.getFieldsValue();
            let params = this.getParams(vals);
            let footer='总调整额(元): '+totalCount;
            let uploadConfig = {
              handleOk: this.handleOk,
              handleCancel: this.handleCancels,
              search: this.search
            }
            const pagination = {
              total:total,
              params:params,
              showTotal:function () {
                return "共" + total + "条数";
              },
              showSizeChanger:true,
              current:pageIndex,
              onShowSizeChange(current,pageSize){
                dispatch({type:'PublishAmountModel/setStateInfo',payload:{pageSize:pageSize}});
                dispatch({type:'PublishAmountModel/getDataList',payload:{}});
              },
              onChange(current){
                dispatch({type:'PublishAmountModel/setStateInfo',payload:{pageIndex:current}});
                dispatch({type:'PublishAmountModel/getDataList',payload:params});
              }
            }
        
            //权限操作
            let tableListOperator = operationArray;
            // Table 配置
            let tableConfig={
              table: (
                <Table  dataSource={list} loading={loading} columns={this.colums} pagination={pagination}
                        rowKey={record => record.id} footer={() =><div>{footer}</div> }/>
              ),
              tableListOperator: tableListOperator
            };
        
            //方法配置
            let methods={
              search: this.search,
              handleFormReset: this.handleFormReset
            };
        
            //查询项 配置
            let userFroms=this.getFroms();
        
            return (
              <div style={{padding: 24,background: '#fff'}}>
                <div className={styles.tableList}>
                  <CompTableList key="PublishAmountModel" tableConfig={tableConfig} methods={methods}
                                 userFroms={userFroms}/>
                  <CompUploadExcel {...this.props} uploadConfig={uploadConfig}/>
                  <UpdateCreateForm
                    wrappedComponentRef={(val)=>this.saveFormRef(val)}
                    visible={this.state.visible}
                    onCancel={()=>this.handleCancel()}
                    HandleUpdate={()=>this.HandleUpdate()}
                    record={this.state.record}
                  />
                </div>
              </div>
            )
          }
    }


    // 调整窗口
    const UpdateCreateForm = Form.create()(
      class extends React.Component {
        constructor(props){
          super(props);
          this.ModalHandleOk = this.ModalHandleOk.bind(this);
          this.state = {
            visible: false,
          }
        }
    
        render() {
          const { visible, onCancel, form,record } = this.props;
          const { getFieldDecorator } = form;
          const { TextArea } = Input;
          const { MonthPicker} = DatePicker;
          const monthFormat = 'YYYY/MM';
          const formItemLayout = {
            labelCol: {
              xs: { span: 4 },
              sm: { span: 8 },
            },
            wrapperCol: {
              xs: { span: 4 },
              sm: { span: 8 },
            },
          };
          if(record===null||record===undefined){   //新建
            return (
              <Modal
                visible={visible}
                title="业绩调整"
                okText="保存"
                onCancel={onCancel}
                onOk={this.ModalHandleOk}
                width={600}
              >
                <Form onSubmit={this.handleSubmit} layout="horizontal">
                  <FormItem
                    {...formItemLayout}
                    label="合同号"
                  >
                    {getFieldDecorator('csn', {
                       initialValue : null,
                        rules: [{
                          required: true, message: '请输入合同号!',
                        }],
                    })(
                      <Input placeholder="请输入" />
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="合同ID"
                  >
                    {getFieldDecorator('contractID', {
                      initialValue : null,
                    })(
                      <Input placeholder="请输入" />
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="数据类型"
                  >
                    {getFieldDecorator('dataType', {
                       initialValue : '请选择',
                    })(
                      <Select placeholder="请选择" style={{ width: 184 }} >
                      <Option value="2">回款</Option>
                      <Option value="1">发布额</Option>
                      </Select>
                    )}
                  </FormItem>
                  <FormItem
                    {...formItemLayout}
                    label="调整业务员"
                  >
                    {getFieldDecorator('userName', {
                       initialValue : null,
                    })(
                      <Input placeholder="请输入" />
                    )}
                  </FormItem>
                  <FormItem
                    {...formItemLayout}
                    label="调整类型:"
                  >
                    {getFieldDecorator('type', {
                       initialValue : '请选择',
                        rules: [{
                          required: true, message: '请选择调整类型!',
                        }],
                    })(
                      <Select placeholder="请选择" style={{ width: 184 }} >
                      <Option value="增加">增加</Option>
                      <Option value="减少">减少</Option>
                      </Select>
                    )}
                  </FormItem>
    
    
                  <FormItem
                    {...formItemLayout}
                    label="调整月份："
                  >
                    {getFieldDecorator('monthPeriod', {
                        initialValue:moment()
                    })(
                      <MonthPicker  placeholder="请选择" style={{ width: 184 }} />
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整后产品线："
                  >
                    {getFieldDecorator('productGroupID', {
                      initialValue : '请选择',
                    })(
                      <Select placeholder="请选择" style={{ width: 184 }} >
                        {
                          Object.keys(ProductGrouNames).map(key=>{
                            return <Option value={key} key={key}>{ProductGrouNames[key]}</Option>
                          })
                        }
                      </Select>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整金额："
                  >
                    {getFieldDecorator('amount', {
                      initialValue : null,
                    })(
                      <InputNumber  placeholder="请输入" style={{ width: 184 }} />
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整原因："
                  >
                    {getFieldDecorator('reason', {
                      initialValue : null,
                    })(
                      <TextArea rows={4} placeholder="请输入" />
                    )}
                  </FormItem>
                </Form>
              </Modal>
            );
          }else {                                  //查看
            return (
              <Modal
                visible={visible}
                title="业绩调整"
                onCancel={onCancel}
                width={600}
                footer={[
                  <Button key="back"  onClick={onCancel}>关闭</Button>
                ]}
              >
                <Form onSubmit={this.handleSubmit} layout="horizontals">
                  <FormItem
                    {...formItemLayout}
                    label="合同号"
                  >
                    {getFieldDecorator('csn', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.csn),
                    })(
                      <label>{record.csn}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="合同业务员"
                  >
                    {getFieldDecorator('saleUser', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.saleUser),
                    })(
                      <label>{record.saleUser}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="数据类型"
                  >
                    {getFieldDecorator('dataType', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.dataType),
                    })(
                      <label>{record.dataType==null?null:(record.dataType==1?'发布额':'回款') }</label>
                    )}
                  </FormItem>
                  <FormItem
                    {...formItemLayout}
                    label="调整业务员"
                  >
                    {getFieldDecorator('userName', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.userName),
                    })(
                      <label>{record.userName}</label>
                    )}
                  </FormItem>
                  <FormItem
                    {...formItemLayout}
                    label="调整类型:"
                  >
                    {getFieldDecorator('type', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.type),
    
                    })(
                      <label>{record.type}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="合同总发布额："
                  >
                    {getFieldDecorator('publishMoney', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.publishMoney),
                    })(
                      <label>{record.publishMoney}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整月份："
                  >
                    {getFieldDecorator('monthPeriod', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.monthPeriod),
                    })(
                      <label>{record.monthPeriod}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整后产品线："
                  >
                    {getFieldDecorator('productGroupName', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.productGroupName),
                    })(
                      <label>{record.productGroupName}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整金额："
                  >
                    {getFieldDecorator('amount', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.amount),
                    })(
                      <label>{record.amount}</label>
                    )}
                  </FormItem>
    
                  <FormItem
                    {...formItemLayout}
                    label="调整原因："
                  >
                    {getFieldDecorator('reason', {
                      initialValue : ((record === '' || record === undefined||record===null) ? '' : record.reason),
                    })(
                      <label>{record.reason}</label>
                    )}
                  </FormItem>
                </Form>
              </Modal>
            );
          }
    
        }
    
        ModalHandleOk () {
          this.props.form.validateFields(
            (err) => {
              if (!err) {
                let vals = this.props.form.getFieldsValue();
    
                debugger;
                this.props.HandleUpdate(vals);
              }
            },
          );
        }
      }
    );


```
