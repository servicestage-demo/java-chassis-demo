# 使用微服务引擎2.0的测试用例

* 参考：https://support.huaweicloud.com/usermanual-cse/cse_03_0001.html 安装微服务引擎2.0

* 设置环境变量:
  * PAAS_CSE_SC_ENDPOINT: 注册中心的地址
  * PAAS_CSE_CC_ENDPOINT: 配置中心的地址

* 依次启动 provider、consumer、gateway

* 在配置中心增加如下配置：
  * 应用级配置：consumer.yaml。类型为 yaml。 

```yaml
cse:
  v2:
    test:
      foo: foo
```

  * 自定义配置：priority1.yaml。label信息： public=default 。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v1
      common: common
```

  * 自定义配置：priority1.yaml。label信息： public=default,extra=default 。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v1
      extra: common
```

  * 应用级配置：priority2.yaml。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v2
```

  * 服务级配置：priority3.yaml，微服务性选择consumer。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v3
```

  * 自定义配置：priority3.yaml，labels: app=demo-java-chassis-cse-v2,environment=,service=consumer,extra=。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v4
```

  * 应用级配置： cse.v2.test.bar: bar 。 类型为 text。 
  
* 执行 tests-client 里面的集成测试用例 （成功）

* 修改
  * priority1.yaml。label信息： public=default 。类型为 yaml。 
```yaml
cse:
  v2:
    test:
      priority: v4
```
