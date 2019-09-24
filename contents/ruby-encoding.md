# ruby **Ruby 中文编码**

---

### 旧版本编码 2.0以下

- Ruby 文件中如果未指定编码，在执行过程会出现报错：

```ruby
#!/usr/bin/ruby -w

puts "你好，世界！";

以上程序执行输出结果为：

invalid multibyte char (US-ASCII) 
```
<div class="fragment fade-in-then-out"><div style="color:red">解决方法为只要在文件开头加入 # -*- coding: UTF-8 -*-（EMAC写法） 或者 #coding=utf-8 就行了</div></div>

<div class="fragment fade-in-then-out">
	<pre>
		<code class="hljs" data-trim data-line-numbers="4,8-11">
#!/usr/bin/ruby -w
# -\*- coding: UTF-8 -*-

puts "你好，世界！";
		</code>
	</pre>
	</div>
---
#### 新版本 
- 默认unicode 编码, 取消$KCODE

```bash
[root@autotest-ruby-agent automationtesting-backend]# irb
2.4.2 :001 > puts "你好，世界！"
你好，世界！
 => nil 
2.4.2 :002 > $KCODE
(irb):2: warning: variable $KCODE is no longer effective
 => nil 


```
