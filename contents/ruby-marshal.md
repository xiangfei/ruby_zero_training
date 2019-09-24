# **Ruby** 序列化

---
## 什么是序列化

- 序列化就是把对象的数据转换成字节流。Ruby 的对象序列化和反序列化是通过 Marshal 这个模块进行的

<aside>
  


</aside>



---

## dump

<aside class="notes">
封送的数据与对象信息一起存储有主版本号和次版本号。在正常使用中，封送处理只能加载使用相同主要版本号和等同或较低次要版本号编写的数据。如果设置了 Ruby 的“详细”标志（通常使用-d，-v，-w 或 -verbose），则主要和次要数字必须完全匹配。元帅版本控制独立于 Ruby 的版本号。您可以通过阅读编组数据的前两个字节来提取版本。
</aside>

- 如果要转储的对象包含绑定，过程或方法对象，类 IO 实例或单例对象，则会引发 TypeError

```ruby

class A

  def s
  end
end

ss = Marshal.dump(AA)

str = Marshal.dump("thing")
str[0].ord     #=> 4
str[1].ord     #=> 8

```
---

## load


```ruby

a = Marshal.load ss

a.s


```


