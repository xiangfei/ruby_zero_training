# **Ruby** 程序安全

---
## 程序漏洞与攻击方法
- DOS(Denial of service)攻击
 - 引起程序异常终止
- 信息泄露
 - 不公开的信息被公开了 
- 权限夺取
- 权限升格


---

## 软件攻击

- shell 注入
-  缓冲区溢出
- 整数溢出
- 跨站点脚本攻击XSS
- SQL注入
- 跨站点伪造请求CSRF
--- 

## shell 注入



```ruby

system("rm -rf /")

```
