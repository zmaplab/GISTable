## 登录

## 菜单

GET: https://api.gistable.com/router

## 一张图

```
GET: https://api.gistable.com/map/{id}
HEADER: PROJECT=64fbced4ed6064f73e992158
```

## 图层控制器

控制图层显示
选中编辑图层

## 快速查询

## 生命周期

入口在基础接口服务， 内部服务的调用编排使用 request/response 模型， 把每个有服务认为是中间件， 上一个中间件的输出， 是下一个中间件的输入

### 创建

#### 成功

```
-> CreateBefore (BizApi) - true -> Create (CoreApi) - true -> CreateAfter (BizApi) - true -+
                                                                                           |
<------------------------------------------------------------------------------------------+
```

#### 预处理失败

前置方法中要注意不得产生脏数据

```
-> CreateBefore (BizApi) - false  -+
                                   |
<----------------------------------+
```

#### 创建失败

若前置方法已经产生数据， 基础服务创建失败， 则应该调用业务的回滚

```
-> CreateBefore (BizApi) - true -> Create (CoreApi) - false  -+
                                                              |
<------------------------------------------------------------ +
```

SAGA 配置

```

```

