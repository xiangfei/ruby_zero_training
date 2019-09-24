# Ruby 方法



</aside>

---

## 无参数方法

<aside class="notes">
- 方法名应以小写字母开头。如果您以大写字母作为方法名的开头，Ruby 可能会把它当作常量，从而导致不正确地解析调用
Ruby 方法与其他编程语言中的函数类似。Ruby 方法用于捆绑一个或多个重复的语句到一个单元中。
</aside>

- def 开头 + 方法名
 - 方法名应以小写字母开头
- end 结尾 



```ruby
def method_name 
   puts "ss"
end

#调用
method_name
```
---

## 参数方法(固定参数)



```ruby
def method_1 (var1, var2)
   p var1 ,  var2
end
def method_2 (var1 = 12, var2= 23)
   p var1, var2
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :306 > method_1 1 , 1
1
1
 => [1, 1] 
2.4.2 :307 > method_1 1 
ArgumentError: wrong number of arguments (given 1, expected 2)
2.4.2 :308 > method_2 
12
23
 => [12, 23] 
2.4.2 :309 > method_2 1
1
23
 => [1, 23] 
2.4.2 :310 > method_2 1 ,2
1
2
 => [1, 2] 
2.4.2 :311 > 

    </code>
  </pre>

</div>

---

## 参数方法 可变参数

```
def method_3(var1 = 12 , *args)
  p  args
end

def method_4(var1  = 12, opts = {})
  p  opts
end
```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">

2.4.2 :302 >   method_3
[]
 => [] 
2.4.2 :303 > method_3 1
[]
 => [] 
2.4.2 :304 > method_3 1 ,2
[2]
 => [2] 
2.4.2 :305 > method_3 1 ,2 ,3 
[2, 3]
 => [2, 3] 
2.4.2 :295 > method_4 4
{}
 => {} 
2.4.2 :296 > method_4 4 , aa: 12 , bb: 22
{:aa=>12, :bb=>22}
 => {:aa=>12, :bb=>22} 
2.4.2 :297 > method_4 4 ,{ aa: 12 , bb: 22}
{:aa=>12, :bb=>22}
 => {:aa=>12, :bb=>22} 
2.4.2 :298 > method_4 4 ,{ :aa=> 12 , :bb => 22}
{:aa=>12, :bb=>22}
 => {:aa=>12, :bb=>22} 
2.4.2 :299 > method_4 4 , :aa=> 12 , :bb => 22
{:aa=>12, :bb=>22}
 => {:aa=>12, :bb=>22} 
    </code>
  </pre>

</div>



---

## 方法 Return
- Ruby 中的 return 语句用于从 Ruby 方法中返回一个或多个值。

```ruby
def test
   i = 100
   j = 200
  return i, j
end
def test1
   i = 100
   return i
   j = 200
end

```


<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">
2.4.2 :324 > p test
[100, 200]
 => [100, 200] 
2.4.2 :325 > p test1
100
 => 100 
    </code>
  </pre>

</div>

---

## 方法 alias
- 这个语句用于为方法或全局变量起别名。别名不能在方法主体内定义。即使方法被重写，方法的别名也保持方法的当前定义。

```bash
2.4.2 :342 >   def sss
2.4.2 :343?>   puts 12
2.4.2 :344?>   end
 => :sss 
2.4.2 :347 > alias  oldss sss
 => nil 
2.4.2 :348 > oldss
12
 => nil
2.4.2 :349 > def sss
2.4.2 :350?>   puts 444
2.4.2 :351?>   end
 => :sss 
2.4.2 :352 > sss
444
 => nil 
2.4.2 :353 > oldss
12

```

---

## 方法 undef

- 取消方法

```bash
2.4.2 :334 > def xxx
2.4.2 :335?>   return 123
2.4.2 :336?>   end
 => :xxx 
2.4.2 :337 > xxx
 => 123 
2.4.2 :338 > undef xxx
 => nil 
2.4.2 :339 > xxx
NameError: undefined local variable or method `xxx' for main:Object
  from (irb):339
  from /usr/local/rvm/rubies/ruby-2.4.2/bin/irb:11:in `<main>'


```

