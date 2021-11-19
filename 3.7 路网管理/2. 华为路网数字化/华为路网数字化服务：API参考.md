## 一、API概览

|         类型         |                         说明                         |
| :------------------: | :--------------------------------------------------: |
|     RSU资源管理      |      包括RSU资源的创建、删除、修改、查询接口。       |
|     RSU型号管理      |    包括RSU设备型号的创建、删除、修改、查询接口。     |
|     IPC资源管理      |               包括IPC资源的查询接口。                |
|     Edge APP管理     |      包括Edge APP的创建、删除、修改、查询接口。      |
|   Edge APP版本管理   | 包括Edge APP版本的创建、删除、修改、更新、查询接口。 |
| Edge APP边缘应用管理 |  包括Edge APP边缘应用的部署、删除、升级、查询接口。  |
|   边缘节点资源管理   |     包括Edge资源的创建、删除、修改、查询等接口。     |
|     业务通道管理     |      包括业务通道的创建、删除、修改、查询接口。      |
|   交通事件资源管理   |      包括交通事件的创建、删除、修改、查询接口。      |
|   V2X MAP资源管理    |                  查询MAP详细信息。                   |
| 数据转发配置资源管理 |     包括kafka配置的创建、删除、更新、查询接口。      |
| 历史交通事件资源管理 |                  查询历史交通事件。                  |
| 即时交通事件资源管理 |                  创建即时交通事件。                  |

### 1.1 RSU资源管理接口

|       API       |               说明                |
| :-------------: | :-------------------------------: |
| 创建多个RSU资源 | 获取路网数字化服务的多个RSU资源。 |
| 创建一个RSU资源 | 创建路网数字化服务的一个RSU资源。 |
| 删除一个RSU资源 | 删除路网数字化服务的一个RSU资源。 |
| 修改一个RSU资源 | 修改路网数字化服务的一个RSU资源。 |

### 1.2 RSU型号管理接口

|       API       |               说明                |
| :-------------: | :-------------------------------: |
|   创建RSU型号   |   创建路网数字化服务的RSU型号。   |
| 查询RSU型号列表 | 查询路网数字化服务的RSU型号列表。 |
|   查询RSU型号   |   查询路网数字化服务的RSU型号。   |
|   修改RSU型号   |   修改路网数字化服务的RSU型号。   |
|   删除RSU型号   |   删除路网数字化服务的RSU型号。   |

### 1.3 IPC资源管理接口

|       API       |               说明                |
| :-------------: | :-------------------------------: |
| 条件查询IPC资源 | 条件查询路网数字化服务的IPC资源。 |
|   查询IPC资源   | 查询路网数字化服务的一个IPC资源。 |

### 1.4 Edge APP管理接口

|     API      |                说明                |
| :----------: | :--------------------------------: |
|   创建应用   |   创建路网数字化服务的Edge应用。   |
|   删除应用   |   删除路网数字化服务的Edge应用。   |
| 查询应用列表 | 查询路网数字化服务的Edge应用列表。 |
|   修改应用   |   修改路网数字化服务的Edge应用。   |

### 1.5 Edge APP版本管理接口

|       API        |                  说明                  |
| :--------------: | :------------------------------------: |
|   创建应用版本   |   创建路网数字化服务的Edge应用版本。   |
|   删除应用版本   |   删除路网数字化服务的Edge应用版本。   |
|   修改应用版本   |   修改路网数字化服务的Edge应用版本。   |
| 查询应用版本列表 | 查询路网数字化服务的Edge应用版本列表。 |
| 查询应用版本详情 | 查询路网数字化服务的Edge应用版本详情。 |
| 更新应用版本状态 | 更新路网数字化服务的Edge应用版本状态。 |

### 1.6 Edge APP边缘应用管理接口

|         API          |                  说明                  |
| :------------------: | :------------------------------------: |
|     部署边缘应用     |     创建路网数字化服务的边缘应用。     |
|   查询边缘应用列表   |   查询路网数字化服务的边缘应用列表。   |
|     升级边缘应用     |     修改路网数字化服务的边缘应用。     |
| 查询边缘应用版本详情 | 查询路网数字化服务的边缘应用版本详情。 |
|     删除边缘应用     |     删除路网数字化服务的边缘应用。     |

### 1.7 边缘节点资源管理接口

|               API               |                       说明                        |
| :-----------------------------: | :-----------------------------------------------: |
|      获取多个V2X Edge资源       |       获取路网数字化服务的多个V2XEdge资源。       |
|        新增V2X Edge资源         |         创建路网数字化服务的V2XEdge资源。         |
|      删除一个V2X Edge 资源      |       删除路网数字化服务的一个V2XEdge资源。       |
|      修改一个V2X Edge资源       |         修改路网数字化服务的V2XEdge资源。         |
|      生成边缘节点安装命令       |      生成路网数字化服务的边缘节点安装指令。       |
| 根据edge_id获取一个V2X Edge资源 | 根据edge_id获取路网数字化服务的一个V2X Edge资源。 |

### 1.8 业务通道管理接口

|     API      |             说明             |
| :----------: | :--------------------------: |
| 创建业务通道 | 创建路网数字化服务业务通道。 |
| 修改业务通道 | 修改路网数字化服务业务通道。 |
| 查询业务通道 | 查询路网数字化服务业务通道。 |
| 删除业务通道 | 删除路网数字化服务业务通道。 |

### 1.9 交通事件资源管理接口

|       API        |                 说明                 |
| :--------------: | :----------------------------------: |
| 条件查询交通事件 |  条件查询路网数字化服务的交通事件。  |
|   新增交通事件   |   新增加路网数字化服务的交通事件。   |
| 查询单个交通事件 | 查询路网数字化服务的单个的交通事件。 |
|   修改交通事件   |    修改路网数字化服务的交通事件。    |
|   删除交通事件   |    删除路网数字化服务的交通事件。    |

### 1.10 V2X Map资源管理接口

|           API           |                    说明                     |
| :---------------------: | :-----------------------------------------: |
|   获取多个V2X MAP资源   |   获取路网数字化服务的多个V2X MAP的资源。   |
| 获取单个V2X MAP节点信息 | 获取路网数字化服务的单个V2X MAP的节点信息。 |

### 1.11 数据转发配置资源管理接口

|       API        |                  说明                   |
| :--------------: | :-------------------------------------: |
| 新增相关配置资源 |  新增路网数字化服务用户kafka配置资源。  |
| 查询多个配置资源 | 获取路网数字化服务的多个kafka配置资源。 |
| 删除一个配置资源 | 删除路网数字化服务的一个kafka配置资源。 |
| 查询一个配置资源 | 获取路网数字化服务的一个kafka配置资源。 |
| 更新一个配置资源 | 更新路网数字化服务的一个kafka配置资源。 |

### 1.12 历史交通事件资源管理接口

|         API          |                  说明                  |
| :------------------: | :------------------------------------: |
| 条件查询历史交通事件 | 条件查询路网数字化服务的历史交通事件。 |

### 1.13 即时交通事件资源管理接口

|       API        |                说明                |
| :--------------: | :--------------------------------: |
| 创建即时交通事件 | 新增路网数字化服务的即时交通事件。 |

## 二、如何调用API

### 2.1 构造请求

#### 请求 URI

请求URI由如下部分组成：

**{URI-scheme}://{Endpoint}/{resource-path}?{query-string}**

尽管请求URI包含在请求消息头中，但大多数语言或框架都要求您从请求消息中单独传递它，所以在此单独强调。

![image-20211119140438013](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119140438013.png)

例如您需要获取IAM在“华北-北京一”区域的Token，则需使用“华北-北京一”区域的Endpoint（iam.cn-north-1.myhuaweicloud.com），并在获取用户Token的URI部分找到resource-path（/v3/auth/tokens），拼接起来如下所示。

> https://iam.cn-north-1.myhuaweicloud.com/v3/auth/tokens

![image-20211119140514257](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119140514257.png)

#### 请求方法

HTTP请求方法（也称为操作或动词），它告诉服务你正在请求什么类型的操作。

![image-20211119140537042](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119140537042.png)

#### 请求消息头

附加请求头字段，如指定的URI和HTTP方法所要求的字段。例如定义消息体类型的请求头“Content-Type”，请求鉴权信息等。

详细的公共请求消息头字段请参见表格内容。

![image-20211119140621522](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119140621522.png)

![image-20211119140634438](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119140634438.png)

对于获取用户Token接口，由于不需要认证，所以只添加“Content-Type”即可，添加消息头后的请求如下所示。

>POST https://iam.cn-north-1.myhuaweicloud.com/v3/auth/tokens 
>
>Content-Type: application/json

#### 请求消息体（可选）

该部分可选。请求消息体通常以结构化格式（如JSON或XML）发出，与请求消息头中Content-Type对应，传递除请求消息头之外的内容。若请求消息体中的参数支持中文，则中文字符必须为UTF-8编码。

每个接口的请求消息体内容不同，也并不是每个接口都需要有请求消息体（或者说消息体为空），GET、DELETE操作类型的接口就不需要消息体，消息体具体内容需要根据具体接口而定。

对于**获取用户Token**接口，您可以从接口的请求部分看到所需的请求参数及参数说明。将消息体加入后的请求如下所示，加粗的斜体字段需要根据实际值填写，其中**username**为用户名，**domainname**为用户所属的帐号名称，**********为用户登录密码，**xxxxxxxxxxxxxxxxxx**为project的名称，如“cn-north-1”，您可以从**地区和终端节点**获取。

**说明**

scope参数定义了Token的作用域，下面示例中获取的Token仅能访问project下的资源。您还可以设置Token额作用域为某个账号下所有资源或账号的某个project下的资源，详细定义请参见**获取用户Token**。

> POST https://iam.cn-north-1.myhuaweicloud.com/v3/auth/tokens 

```json
Content-Type: application/json
{ 
    "auth": { 
        "identity": { 
            "methods": [ 
                "password" 
            ], 
            "password": { 
                "user": { 
                    "name": "username", 
                    "password": "********", 
                    "domain": { 
                        "name": "domainname" 
                    } 
                } 
            } 
        }, 
        "scope": { 
            "project": { 
                "name": "xxxxxxxxxxxxxxxxx" 
            } 
        } 
    } 
}
```

到这里为止这个请求需要的内容就具备齐全了，您可以使用**curl**、**Postman**或直接编写代码等方式发送请求调用API。对于获取用户Token接口，返回的响应消息头中“x-subject-token”就是需要获取的用户Token。有了Token之后，您就可以使用Token认证调用其他API。

### 2.2 认证鉴权

调用接口有如下两种认证方式，您可以选择其中一种进行认证鉴权。

● Token认证：通过Token认证通用请求。

● AK/SK认证：通过AK（Access Key ID）/SK（Secret Access Key）加密调用请求。

推荐使用AK/SK认证，其安全性比Token认证要高。

#### Token 认证

Token是服务端生成的一串字符串，作为客户端进行请求的一个令牌。第一次登录后，服务器生成一个Token并将此Token返回给客户端，以后客户端只需带上这个Token前来请求数据即可，无需再次带上用户名和密码。Token有效期是24小时，从客户端获取开始算起（24小时是相对时间），需要使用同一个Token鉴权时，建议缓存起来使用，避免频繁调用。在Token过期前，务必刷新Token或重新获取Token，否则Token过期后会在服务端鉴权失败。

如果您获取Token多次，以最新的为准，前面的Token会被覆盖并失效。

Token在计算机系统中代表令牌（临时）的意思，拥有Token就代表拥有某种权限。

Token认证就是在调用API的时候将Token加到请求消息头，从而通过身份认证，获得操作API的权限。

Token可通过调用**获取用户Token**接口获取，调用本服务API需要project级别的Token，即调用**获取用户Token**接口时，请求body中auth.scope的取值需要选择project，如下所示。

```json
{ 
    "auth": { 
        "identity": { 
            "methods": [ 
                "password" 
            ], 
            "password": { 
                "user": { 
                    "name": "username", 
                    "password": "********", 
                    "domain": { 
                        "name": "domainname" 
                    } 
                } 
            } 
        }, 
        "scope": {
            "project": {
                "name": "xxxxxxxxxxxxxxxxxxxxxx"
            }
        }
    } 
}
```

说明：加粗的斜体字段需要根据实际值填写，其中**username**为IAM用户名，**domainname**为IAM用户所属帐号名，***\**\**\**\***为IAM用户的登录密码，**xxxxxxxxx**为IAM用户所属账号的项目名称，如“cn-north-1”，您可以参考**我的凭证**页面获取。

接口返回的响应消息头中“X-Subject-Token”就是需要获取的用户Token。

获取Token后，再调用其他接口时，您需要在请求消息头中添加“X-Auth-Token”，其值为获取到的Token。例如Token值为“ABCDEFJ....”，则调用接口时将“X-Auth-Token: ABCDEFJ....”加到请求消息头即可，如下所示。

#### AK/SK 认证

AK/SK签名认证方式仅支持消息体大小12MB以内，12MB以上的请求请使用Token认证。

AK/SK认证就是使用AK/SK对请求进行签名，在请求时将签名信息添加到消息头，从而通过身份认证。

● AK（Access Key ID）：访问密钥ID。与私有访问密钥关联的唯一标识符；访问密钥ID和私有访问密钥一起使用，对请求进行加密签名。

● SK（Secret Access Key）：与访问密钥ID结合使用的密钥，对请求进行加密签名，可标识发送方，并防止请求被修改。

使用AK/SK认证时，您可以基于签名算法使用AK/SK对请求进行签名，也可以使用专门的签名SDK对请求进行签名。详细的签名方法和SDK使用方法请参见**API签名指南**。

**须知**：签名SDK只提供签名功能，与服务提供的SDK不同，使用时请注意。

### 2.3 返回结果

#### 2.3.1 状态码

请求发送以后，您会收到响应，包含状态码、响应消息头和消息体。

状态码是一组从1xx到5xx的数字代码，状态码表示了请求响应的状态，完整的状态码列表请参见**状态码**。

对于**获取用户Token**接口，如果调用后返回状态码为“201”，则表示请求成功。

**响应消息头**

对应请求消息头，响应同样也有消息头，如“Content-type”等。

对于**获取用户Token**接口，返回如下图所示的消息头，其中**“x-subject-token”**就是需要获取的用户Token。有了Token之后，您就可以使用Token认证调用其他API。

#### 2.3.2 响应消息体（可选）

该部分可选。响应消息体通常以结构化格式（如JSON或XML）返回，与响应消息头中Content-Type对应，传递除响应消息头之外的内容。

对于**获取用户Token**接口，返回如下消息体。为篇幅起见，这里只展示部分内容。

```json
{ 
    "token": { 
        "expires_at": "2019-02-13T06:52:13.855000Z", 
        "methods": [ 
            "password" 
        ], 
        "catalog": [ 
            { 
                "endpoints": [ 
                    { 
                        "region_id": "cn-north-1",
```

当接口调用出错时，会返回错误码及错误信息说明，错误响应的Body体格式如下所示。

```json
{
    "error_code": "DRIS.01010002",
    "error_msg": "The RSU not found. "
}
```

其中，error_code表示错误码，error_msg表示错误描述信息。

## 三、API

### 3.1 RSU资源管理

#### 3.1.1 获取多个 RSU 资源

**功能介绍**

获取多个RSU资源

**URI**

GET /v1/{project_id}/rsus

![image-20211119152924926](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119152924926.png)

![image-20211119152942655](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119152942655.png)

![image-20211119153032967](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153032967.png)

#### 3.1.2 创建一个RSU资源

**功能介绍**

创建一个RSU资源

**URI**

POST /v1/{project_id}/rsus

![image-20211119153114567](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153114567.png)

![image-20211119153139264](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153139264.png)

#### 3.1.3 删除一个RSU资源

**功能介绍**

删除一个RSU资源

**URI**

DELETE /v1/{project_id}/rsus/{rsu_id}

#### 3.1.4 修改一个RSU资源

**功能介绍**

修改一个RSU资源

**URI**

PUT /v1/{project_id}/rsus/{rsu_id}

![image-20211119153242152](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153242152.png)

**响应参数**

**状态码：** **200**

![image-20211119153320951](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153320951.png)

### 3.2 RSU型号管理

该章节仅供使用了非华为RSU设备的用户参考。使用华为RSU设备的用户需跳过此章节。

#### 3.2.1 创建 RSU 型号

**功能介绍**

调用此接口可创建RSU型号。

**URI**

POST /v1/{project_id}/rsu-models

![image-20211119153426839](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153426839.png)

**响应参数**

**状态码：** **201**

![image-20211119153456176](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153456176.png)

**请求示例**

```json
POST https://{endpoint}/v1/{project_id}/rsu-models
{
 "rsu_model_id" : "5ba24f5ebbe8f56f5a14f605",
 "name" : "RSU001",
 "manufacturer_name" : "ABC",
 "description" : "excellent"
}
```

**响应示例**

**状态码：** **201**

Created

```json
{
 "rsu_model_id" : "5ba24f5ebbe8f56f5a14f605",
 "name" : "RSU001",
 "manufacturer_name" : "ABC",
 "description" : "excellent",
 "created_time" : "2020-12-07T01:32:17.387Z"
}
```

#### 3.2.2 查询 RSU 型号列表

**功能介绍**

可调用此接口查询已导入RSU型号列表。

**URI**

GET /v1/{project_id}/rsu-models

![image-20211119153635156](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153635156.png)

**响应参数**

**状态码：** **200**

![image-20211119153703487](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153703487.png)

![image-20211119153722425](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153722425.png)

#### 3.2.3 查询RSU型号

**功能介绍**

可调用此接口查询已导入的RSU型号。

**URI**

GET /v1/{project_id}/rsu-models/{rsu_model_id}

**响应参数**

**状态码：** **200**

![image-20211119153819888](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153819888.png)

#### 3.2.4 修改RSU型号

**功能介绍**

可调用此接口修改已导入的RSU型号。

**URI**

PUT /v1/{project_id}/rsu-models/{rsu_model_id}

![image-20211119153903743](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153903743.png)

**响应参数**

**状态码：** **200**

![image-20211119153922951](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119153922951.png)

#### 3.2.5 删除RSU型号

**功能介绍**

可调用此接口删除已导入的RSU型号。

**URI**

DELETE /v1/{project_id}/rsu-models/{rsu_model_id}

### 3.3 IPC资源

#### 3.3.1 条件查询IPC资源

**功能介绍**

获取多个IPC资源

**URI**

GET /v1/{project_id}/cameras

![image-20211119154025776](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154025776.png)

**响应参数**

**状态码：** **200**

![image-20211119154046545](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154046545.png)

![image-20211119154119031](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154119031.png)

#### 3.3.2 查询IPC资源

**功能介绍**

查询IPC资源

**URI**

GET /v1/{project_id}/cameras/{camera_id}

**响应参数**

**状态码：** **200**

![image-20211119154230249](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154230249.png)

![image-20211119154241553](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154241553.png)

### 3.4 Edge APP管理

#### 3.4.1 创建应用

**功能介绍**

创建应用

**URI**

POST /v1/{project_id}/v2x-edge-apps

![image-20211119154329151](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154329151.png)

**响应参数**

**状态码：** **201**

![image-20211119154345152](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154345152.png)

#### 3.4.2 删除应用

**功能介绍**

删除应用

**URI**

DELETE /v1/{project_id}/v2x-edge-apps/{edge_app_id}

#### 3.4.3 查询应用列表

**功能介绍**

查询应用列表

**URI**

GET /v1/{project_id}/v2x-edge-apps

![image-20211119154433039](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154433039.png)

**响应参数**

**状态码：** **200**

![image-20211119154452407](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154452407.png)

![image-20211119154459257](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154459257.png)

#### 3.4.4 修改应用

**功能介绍**

修改应用

**URI**

PUT /v1/{project_id}/v2x-edge-apps/{edge_app_id}

**响应参数**

**状态码：** **200**

![image-20211119154541496](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119154541496.png)

### 3.5 Edge 版本管理



### 3.6 Edge APP边缘应用管理

#### 3.6.1 部署边缘应用

**功能介绍**：部署边缘应用

**URI**

POST /v1/{project_id}/v2x-edges/{v2x_edge_id}/apps

### 3.7 边缘节点资源管理

#### 3.7.1 获取多个V2X Edge资源

**功能介绍**

获取多个V2XEdge资源

**URI**

GET /v1/{project_id}/v2x-edges

#### 3.7.2 新增V2x Edge资源





### 3.9 交通事件资源管理

#### 3.9.1 条件查询交通事件

**功能介绍**

条件查询交通事件

**URI**

GET /v1/{project_id}/traffic-events

![image-20211119155129485](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155129485.png)

![image-20211119155139073](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155139073.png)

**响应参数**

**状态码：** **200**

![image-20211119155221303](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155221303.png)

![image-20211119155244793](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155244793.png)

![image-20211119155304688](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155304688.png)

![image-20211119155322584](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155322584.png)

#### 3.9.2 新增交通事件

**功能介绍**

新增交通事件

**URI**

POST /v1/{project_id}/traffic-events

![image-20211119155437608](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155437608.png)

![image-20211119155518912](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155518912.png)

![image-20211119155539835](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155539835.png)

![image-20211119155603791](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155603791.png)

![image-20211119155615767](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155615767.png)

#### 3.9.3 查询单个交通事件

**功能介绍**

查询单个交通事件

**URI**

GET /v1/{project_id}/traffic-events/{event_id}

**响应参数**

**状态码：** **200**

![image-20211119155719848](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155719848.png)

![image-20211119155729417](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155729417.png)

![image-20211119155738256](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155738256.png)

#### 3.9.4 修改交通事件

**功能介绍**

修改交通事件

**URI**

PUT /v1/{project_id}/traffic-events/{event_id}

![image-20211119155828601](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155828601.png)

![image-20211119155838130](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155838130.png)

![image-20211119155849895](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155849895.png)

**响应参数**

**状态码：** **200**

![image-20211119155903149](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155903149.png)

![image-20211119155911719](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155911719.png)

![image-20211119155922288](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155922288.png)

![image-20211119155931341](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119155931341.png)

#### 3.9.5 删除交通事件

**功能介绍**

刪除交通事件

**URI**

DELETE /v1/{project_id}/traffic-events/{event_id}





### 3.11 数据转发配置资源管理

#### 3.11.1 新增相关配置资源

**功能介绍**

新增用户kafka配置资源

**URI**

POST /v1/{project-id}/forwarding-configs

![image-20211119161351880](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161351880.png)

![image-20211119161410833](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161410833.png)

**响应参数**

**状态码：** **201**

![image-20211119161425440](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161425440.png)

![image-20211119161436905](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161436905.png)

#### 3.11.2 查询多个配置资源

**功能介绍**

查询多个kafka配置资源

**URI**

GET /v1/{project_id}/forwarding-configs



### 3.12 历史交通事件资源管理

#### 3.12.1 条件查询历史交通事件

**功能介绍**

条件查询历史交通事件

**URI**

GET /v1/{project_id}/history-traffic-events

![image-20211119161657978](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161657978.png)

**响应参数**

**状态码：** **200**

![image-20211119161737112](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161737112.png)

![image-20211119161746264](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161746264.png)

![image-20211119161757760](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161757760.png)

**请求示例**

```
GET https://{endpoint}/v1/{project_id}/history-traffic-events
```

### 3.13 即时交通事件资源管理

#### 3.13.1 创建即时交通事件

**功能介绍**

创建即时交通事件

**URI**

POST /v1/{project_id}/immediate-event

![image-20211119161948672](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161948672.png)

![image-20211119161958079](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161958079.png)

![image-20211119162005775](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162005775.png)

![image-20211119162016296](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162016296.png)

**响应参数**

**状态码：** **201**

![image-20211119162030496](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162030496.png)

![image-20211119162045968](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162045968.png)

![image-20211119162059865](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162059865.png)

![image-20211119162122535](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119162122535.png)

## 四、应用示例

### 4.1 创建一个RSU资源

**操作场景**

路网数字化服务要实现接收和广播交通事件，需要创建路侧通信单元RSU。

下面介绍如何调用API创建一个RSU资源，API的调用方法请参见**如何调用API**。

**前提条件**

您需要规划RSU所在的区域信息，并根据区域确定调用API的Endpoint，详细信息请参见**地区与终端节点**。

当前路网数字化服务的区域仅支持华北-北京四，终端节点**“ocv2x-api.cn-north-4.myhuaweicloud.com"**。

**操作步骤**

**步骤1** 创建一个RSU资源。

● 接口相关信息

URI格式：POST https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/{project_id}/rsus

请求参数说明详情，请参见**创建一个RSU资源**。 

● 请求示例

POST：https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/060f5d9b5c000fc22f2ec014e79641cb/rsus

Body： 

```json
{
 "name": "示例1",
 "description": "示例",
 "esn": "123",
 "ip": "127.0.0.1",
 "position_description": "K08",
 "related_edge_num": 1
}
```

● 响应示例

```json
{
    "rsu_id": "b0b22a06-c4e1-4c2b-a7f6-fa9bd8269f80",
    "name": "示例1",
    "description": "示例",
    "esn": "123",
    "last_modified_time": "2021-04-07T07:50:39Z",
    "created_time": "2021-04-07T07:50:39Z",
    "ip": "127.0.0.1",
    "position_description": "K08",
    "status": "INITIAL",
    "related_edge_num": 1
}
```

**步骤2** 确认RSU创建成功。

● 接口相关信息

URI格式：GET https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/{project_id}/rsus

请求参数说明详情，请参见**获取多个RSU资源**。 

● 请求示例

GET：https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/060f5d9b5c000fc22f2ec014e79641cb/rsus

● 响应示例

```json
{
    "count": 2,
    "rsus": [
        {
            "rsu_id": "b0b22a06-c4e1-4c2b-a7f6-fa9bd8269f80",
            "name": "示例1",
            "description": "示例",
            "esn": "123",
            "last_modified_time": "2021-04-07T07:50:39Z",
            "created_time": "2021-04-07T07:50:39Z",
            "ip": "127.0.0.1",
            "position_description": "K08",
            "status": "INITIAL",
            "related_edge_num": 1
        },
        ...
    ]
}
```

### 4.2 创建一个Edge资源

**操作场景**

路网数字化服务要实现边缘事件算法部署、路侧传感器接入管理、路侧传感器数据融合分析、边缘事件通信分发等功能，需要创建边缘计算单元Edge。

下面介绍如何调用API创建一个Edge资源，API的调用方法请参见**如何调用API**。

**前提条件**

您需要规划Edge所在的区域信息，并根据区域确定调用API的Endpoint，详细信息请参见**地区与终端节点**。

当前路网数字化服务的区域仅支持华北-北京四，终端节点**“ocv2x-api.cn-north-4.myhuaweicloud.com”**。

**操作步骤**

**步骤1** 创建一个Edge资源。

● 接口相关信息

URI格式：POST https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/{project_id}/v2x-edges

请求参数说明详情，请参见**新增V2XEdge资源**。 

● 请求示例

POST：POST https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/060f5d9b5c000fc22f2ec014e79641cb/v2x-edges

Body： 

```json
{
    "name": "示例1",
    "description": "示例",
    "esn": "123",
    "ip": "127.0.0.0",
    "position_description": "K08",
    "location": {
        "lat": 10,
        "lon": 20
    },
    "edge_general_config": {
        "avp_enabled": false,
        "rsm_enabled": false,
        "time_compensate": false
    }
}
```

● 响应示例

```json
{
    "v2x_edge_id": "a78e11ed-38dd-4a36-aa60-1c8652bed7f7",
    "name": "示例1",
    "description": "示例",
    "esn": "123",
    "ip": "127.0.0.0",
    "position_description": "K08",
    "camera_ids": [],
    "radar_ids": [],
    "local_rsus": [],
    "edge_general_config": {
        "avp_enabled": false,
        "rsm_enabled": false,
        "time_compensate": false
    },
    "status": "UNINSTALLED",
    "node_id": "577220960881750016",
    "created_time": "2021-04-07T09:11:07Z",
    "last_modified_time": "2021-04-07T09:11:07Z"
}
```

**步骤2** 确认Edge创建成功。

● 接口相关信息

URI格式：GET https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/{project_id}/v2x-edges

请求参数说明详情，请参见**获取多个V2XEdge资源**。 

● 请求示例

GET：https://ocv2x-api.cn-north-4.myhuaweicloud.com/v1/060f5d9b5c000fc22f2ec014e79641cb/v2x-edges

● 响应示例

```json
{
    "count": 11,
    "edges": [
        {
            "v2x_edge_id": "a78e11ed-38dd-4a36-aa60-1c8652bed7f7",
            "name": "示例1",
            "esn": "123",
            "position_description": "K08",
            "status": "UNINSTALLED",
            "created_time": "2021-04-07T09:11:07Z"
        },
        ...
    ]
}
```

### 5.3 新增交通事件

**操作场景**

路网数字化服务支持平台下发交通事件和手动上报交通事件。

下面介绍如何调用API手动上报交通事件，API的调用方法请参见**如何调用API**。

**前提条件**

您需要规划Edge所在的区域信息，并根据区域确定调用API的Endpoint，详细信息请参见**地区与终端节点**。

当前路网数字化服务的区域仅支持华北-北京四，终端节点**“ocv2x-api.cn-north-4.myhuaweicloud.com”**。

**操作步骤**

**步骤1** 新增一个交通事件。

● 接口相关信息

URI格式：POST https://xxxxxxx/v1/{project_id}/traffic-events

请求参数说明详情，请参见**新增交通事件**。 

● 请求示例

POST：POST  https://xxxxxxx/v1/060f59b5c000fc22f2c01479641cbȍìrfficȝvnìä

Body： 

```json
{
    "event_source_type": "unknown",
    "event_source_id": "示例1",
    "event_class": ȊbnÑrmÃfrfficȊȀ
    "event_type": 1,
    "area_code": 440300,
    "event_level": 1,
    "event_position": {
    "lat": 10,
    "lon": 20
},
"reference_paths": [
    {
        "active_path": [
            {
                "lat": 10,
                "lon": 20
            }
        ]
    }
],
"event_position_name": "示例1",
"start_time": "2020-09-01T01:37:01Z",
"end_time": "2020-09-01T03:37:01Z"
}
```

● 响应示例

```json
{
    "status": "Invalid",
    "event_id": Ȋb859b9b7ȝ981ȝ486ȝ9cȝ78ff3519027ȊȀ
    "event_source_type": "unknown",
    "event_source_id": "示例1",
    "event_class": Ȋfrffic^²gnȊȀ
    "event_type": 1,
    "area_code": 440300,
    "event_level": 1,
    "event_params": {},
"event_position": {
    "lat": 10,
    "lon": 20
},
"reference_paths": [
    {
        "active_path": [
            {
                "lat": 10,
                "lon": 20
            }
        ],
        "path_radius": 1000
    }
],
"event_position_name": "示例1",
"start_time": "2020-09-01T01:37:01Z",
"end_time": "2020-09-01T03:37:01Z",
"created_time": "2021-04-08T02:26:18Z",
"last_modified_time": "2021-04-08T02:26:18Z"
}
```

**步骤2** 确认交通事件新增成功。

● 接口相关信息

URI格式：GET  https://xxxxxxxxxxxx/v1/{project_id}/traffic_events/{event_id}

请求参数说明详情，请参见**查询单个交通事件**。 

● 请求示例

GET：https://xxxxxxxxxxxx/v1/{project_id}/traffic_events/{event_id}

● 响应示例

```json
{
    "status": "Invalid",
    "event_id": Ȋb859b9b7ȝ981ȝ486ȝ9cȝ78ff3519027ȊȀ
    "event_source_type": "unknown",
    "event_source_id": "示例1",
    "event_class": Ȋfrffic^²gnȊȀ
    "event_type": 1,
    "area_code": 440300,
    "event_level": 1,
    "event_params": {},
"event_position": {
    "lat": 10,
    "lon": 20
},
"reference_paths": [
    {
        "active_path": [
            {
                "lat": 10,
                "lon": 20
            }
        ],
        "path_radius": 1000
    }
],
"event_position_name": "示例1",
"start_time": "2020-09-01T01:37:01Z",
"end_time": "2020-09-01T03:37:01Z",
"created_time": "2021-04-08T02:26:18Z",
"last_modified_time": "2021-04-08T02:26:18Z"
}
```

