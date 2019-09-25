# **Ruby** rdoc


---

## rdoc是什么

- 用来创建ruby doc 文档

<aside class="notes">
	rvm docs generate

</aside>

---

# command

```
rdoc  folder 

```
---

## demo


```ruby
class Device_testsuit
  #用例名称：高级管理员的账号密码正确性和权限
  # 作者:gaobiao/A317
  #
  # 预设条件：设备已经按照要求完成初始化
  # 用例步骤：
  ##1. 使用高级用户和密码登录luci
  ##2. 检查页面用户能看到的菜单及功能
  # 预期结果：
  ##1. 登录成功
  ##2. “aWiFi配置”的二级菜单由“个性化站点、aWiFi无线网络（仅对无线终端适用）、LAN侧认证配置、个>性化站点服务器、默认服务器以及自动升级配置”组成

  def test_S_Dev_More_001
      puts "adasdas"
  end

end

```

---

## ri 

- 查看方法


```ruby
ri String

```
