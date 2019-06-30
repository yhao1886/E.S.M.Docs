# API文档

## 用户接口

## 用户查看问卷

method: GET

api: '/api/v1/user_questionnaire'

params:
- page: 第几页数据，默认1
- limit: 每页数据默认10
- status: 状态， 默认草稿
- with_detail: 是否需要详情，默认False
- id：问卷id，默认空

respond：
```json
{
    "pages":100,//总页数
    "count":8888,//问卷总数
    "objs":[//问卷列表
        {
            "id": 1,//问卷id
            "title": "测试问卷",//问卷标题
            "quantity":100,//问卷数量
            "free_quantity":100,//剩余问卷数量
            "expire_date":"2018-12-10",//问卷截止时间
            "create_date":"2018-7-4",//问卷创建时间
            "status":0,//问卷状态：0->草稿，1->待审核，2->审核失败，3->审核通过，4->已发布
            "customer":{
                "id":1,//
                "name":""//
            },
            "questions":[
                {
                    "id":1,//选项id
                    "title":"问题1",//问题标题
                    "category":"radio",//问题类型，radio为单选，checkbox为多选
                    "items":[
                        {
                            "id": 1,//选项id
                            "content":"选项1",//选项1
                        }
                    ]
                },
                
            ],
            "comments":[//批注信息
                {
                    "id":1,//批注id
                    "create_date":"2018-7-5",//批注日期
                    "content":"测试批注不通过",//批注内容
                }
            ]
        }
    ]
}
```
 
## 参与信息

### 参与问卷

method: PUT

api: '/api/v1/participation'

body:
- **questionnaire_id**: 问卷id

response:
```json
{
  "msg":"参与成功"
}
```

### 退出参与

method: DELETE

api: '/api/v1/participation'

body:

- **ids**: 参与信息id列表，例如ids:[1,2,3]

response:
```json
{
  "delete_ids":[2,3]
}
```

## 用户查看参与信息

method: GET

api: `/api/v1/participation`

body:
- state: 参与信息状态, 默认False
- page: 第几页，默认1
- limit: 每业数量， 默认10

response:
```json
{
    "questionnaire": {
        "title": "问卷1" //问卷标题
    },
    "join_date": "2018-10-10", //参与时间
    "state": false //参与状态，false未完成，true已完成
}
```

## 答案

### 提交答案

method: PUT

api: '/api/v1/answer'

body:
- **item_id**:选项id

response:
```json
{
  "msg":"提交成功"
}
```


### 删除答案

method: DELETE

api: '/api/v1/answer'

body:
- **item_ids**: 选项id列表，如ids:[1,2,3]

response:
```json
{
  "delete_ids":[2,3]
}
```

## 用户查看问卷答案

method: GET

api: `/api/v1/user_answer`

body:
- **questionnaire_id**: 问卷id

response:
```json
{
    "questionnaire": {
        "title": "测试问卷", //问卷标题
        "deadline": "2018-10-10", //问卷截止信息
        "customer": "前锋" //问卷所属客户名称
    },
    "questions": [
        {
            "title": "问题1", //问题
            "category": "radio", //问题类型，radio单选，select多选
            "id": 1, //问题id
            "items": [
                {
                    "id": 1, //选项id
                    "content": "选项1", //选项内容
                    "is_select": false //是否选择了选项
                },
                ......
            ]
        }
    ]
}
```

## 用户完成答题

method: POST

api: `/api/v1/user_participation_state`

body:
- **questionnaire_id**: 问卷id

response:
```json
{
    "msg": "提交成功"
}
```

## 用户查看积分

method: GET

api: `/api/v1/user_point_history`

body:
- category: 积分类型，false代表消费，true代表获取，默认true
- page: 第几页， 默认1
- limit: 每页数量，默认10

response:
```json
{
    "balance": 1000, //用户积分数量
    "history": [
        {
            "create_date": "2018-10-10", //历史时间
            "amount": 10, //数量
            "reason": "提交问卷" //原因
        },
        ......
    ]
}
```
## 支付回调接口

method: [GET, POST]

body:
- **order_ids**: 内部订单号
- **amount**: 支付金额
- **state**: 是否支付成功

response:根据第三方需求，返回相应的数据
# 客户接口
## 问卷接口

## 创建问卷

method:PUT

api: '/api/v1/customer_questionnaire'

body:
- **title**: 问卷标题
- **expire_date**: 截至时间格式是：YYYY-MM-DD, 例如：2018-10-20
- **quantity**:数量

response:
```json
{
    "id":1 //新建的问卷id

}
```

## 更新问卷

method:POST

api: '/api/v1/customer_questionnaire'

body:
- **id**: 问卷id
- **title**:问卷标题
- **expire_date**: 截止时间，格式是：YYYY-MM-DD,例如：2018-10-20
- **quantity**:数量

response:
```json
{
    "msg":"更新成功"
}
```

## 删除问卷

method: DELETE

api: '/api/v1/customer_questionnaire'

body:

- **ids**:删除的问卷id列表， 例如{"ids":[1,2,3,4]}

response:
```json
{
    "delete_ids":[2,4] //被删除的问卷id列表
}
```

## 获取问卷

method: GET

api: '/api/v1/customer_questionnaire'

params:
- page: 第几页数据，默认1
- limit: 每页数据默认10
- status: 状态， 默认草稿
- with_detail: 是否需要详情，默认False
- id：问卷id，默认空

respond：
```json
{
    "pages":100,//总页数
    "count":8888,//问卷总数
    "objs":[//问卷列表
        {
            "id": 1,//问卷id
            "title": "测试问卷",//问卷标题
            "quantity":100,//问卷数量
            "free_quantity":100,//剩余问卷数量
            "expire_date":"2018-12-10",//问卷截止时间
            "create_date":"2018-7-4",//问卷创建时间
            "status":0,//问卷状态：0->草稿，1->待审核，2->审核失败，3->审核通过，4->已发布
            "customer":{
                "id":1,//
                "name":""//
            },
            "questions":[
                {
                    "id":1,//选项id
                    "title":"问题1",//问题标题
                    "category":"radio",//问题类型，radio为单选，checkbox为多选
                    "items":[
                        {
                            "id": 1,//选项id
                            "content":"选项1",//选项1
                        }
                    ]
                },
                
            ],
            "comments":[//批注信息
                {
                    "id":1,//批注id
                    "create_date":"2018-7-5",//批注日期
                    "content":"测试批注不通过",//批注内容
                }
            ]
        }
    ]
}
```

## 问题接口

### 创建问题

method: PUT

api: '/api/v1/customer_question'

body:
- questionnaire_id: 问卷id
- title: 问题
- category： radio或者checkbox
- **items** ['选项一','选项二'，'选项三']

response：
```json
    {
      "id":1
    }

```


### 更新问题

method: POST

api: '/api/v1/customer_question'

body:
- id: 问题id
- title: 问题
- category： radio或者checkbox
- **items** ['选项一','选项二'，'选项三']

response：
```json
{
  "msg":"更新成功"
}

```


### 删除问题

method: DELETE

api: '/api/v1/customer_question'

body:
- **ids**: 问卷id  ids:[1,2,3]


response：
```json
{
  "delete_ids":[2,4]
}

```


##  问卷状态

### 修改问卷状态

method:POST

api: '/api/v1/questionnaire_state'

body:
- **id**: 问卷id
- **state** 问卷状态

>  本接口用于：
>- 问卷提交审核：将问卷状态改为1，
>- 问卷发布：蒋问卷状态改为4

response:
```json
{
  "msg":"修改成功"
}
```

## 客户发起支付请求

method: PUT

api: `/api/v1/payment`

body: 
- **amount**:金额

response:
```json
{
    "qrcode": "ivosdjfsofsdfsdf=", //支付信息二维码， 使用方式<img src="data:img/png;base64, ivosdjfsofsdfsdf="
}
```

## 客户钱包流水

method: GET

api: `/api/v1/customer_wallet_flow`

body：
- page: 第几页,默认1
- limit: 每页数量，默认10
- category: 流水类型, false代表消费, true代表支付

response:
```json
{
    "id": 1, //流水id
    "create_date": "2018-01-01", //发生时间
    "amount": 100, //金额
    "reason": "支付宝扫码支付", //原因
    "state": false, //false,未完成，true，已完成
    "category": false //类型
}
```

