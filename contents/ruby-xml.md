# **Ruby** XML

---
## 什么是 XML


<aside class="notes">
	
- 生成套接字，主要有3个参数：通信的目的IP地址、使用的传输 层协议(TCP或UDP)和使用的端口号。Socket原意是"插座"。通过将这3个参数结合起来，与一个"插座"Socket绑定，应用层就可以和传输 层通过套接字接口，区分来自不同应用程序进程或网络连接的通信，实现数据传输的并发服务。

</aside>

- XML 指可扩展标记语言（eXtensible Markup Language）。
可扩展标记语言，标准通用标记语言的子集，一种用于标记电子文件使其具有结构性的标记语言
- 它可以用来标记数据、定义数据类型，是一种允许用户对自己的标记语言进行定义的源语言。 它非常适合万维网传输，提供统一的方法来描述和交换独立于应用程序或供应商的结构化数据。

---

## XML解析器结构和API


<aside class="notes">

</aside>

- SAX解析器是基于事件处理的，需要从头到尾把XML文档扫描一遍，在扫描的过程中，每次遇到一个语法结构时，就会调用这个特定语法结构的事件处理程序，向应用程序发送一个事件。
- DOM是文档对象模型解析，构建文档的分层语法结构，在内存中建立DOM树，DOM树的节点以对象的形式来标识，文档解析文成以后，文档的整个DOM树都会放在内存中
---

## Ruby 中解析及创建 XML

- DOM 解析器


<aside class="notes"> 

<collection shelf="New Arrivals">
<movie title="Enemy Behind">
   <type>War, Thriller</type>
   <format>DVD</format>
   <year>2003</year>
   <rating>PG</rating>
   <stars>10</stars>
   <description>Talk about a US-Japan war</description>
</movie>
<movie title="Transformers">
   <type>Anime, Science Fiction</type>
   <format>DVD</format>
   <year>1989</year>
   <rating>R</rating>
   <stars>8</stars>
   <description>A schientific fiction</description>
</movie>
   <movie title="Trigun">
   <type>Anime, Action</type>
   <format>DVD</format>
   <episodes>4</episodes>
   <rating>PG</rating>
   <stars>10</stars>
   <description>Vash the Stampede!</description>
</movie>
<movie title="Ishtar">
   <type>Comedy</type>
   <format>VHS</format>
   <rating>PG</rating>
   <stars>2</stars>
   <description>Viewable boredom</description>
</movie>
</collection>
</aside>

```ruby 
#!/usr/bin/ruby -w
 
require 'rexml/document'
include REXML
 
xmlfile = File.new("movies.xml")
xmldoc = Document.new(xmlfile)
 
# 获取 root 元素
root = xmldoc.root
puts "Root element : " + root.attributes["shelf"]
 
# 以下将输出电影标题
xmldoc.elements.each("collection/movie"){ 
   |e| puts "Movie Title : " + e.attributes["title"] 
}
 
# 以下将输出所有电影类型
xmldoc.elements.each("collection/movie/type") {
   |e| puts "Movie Type : " + e.text 
}
 
# 以下将输出所有电影描述
xmldoc.elements.each("collection/movie/description") {
   |e| puts "Movie Description : " + e.text 
}

```




---

## SAX 解析器


```ruby

#!/usr/bin/ruby -w
 
require 'rexml/document'
require 'rexml/streamlistener'
include REXML
 
 
class MyListener
  include REXML::StreamListener
  def tag_start(*args)
    puts "tag_start: #{args.map {|x| x.inspect}.join(', ')}"
  end
 
  def text(data)
    return if data =~ /^\w*$/     # whitespace only
    abbrev = data[0..40] + (data.length > 40 ? "..." : "")
    puts "  text   :   #{abbrev.inspect}"
  end
end
 
list = MyListener.new
xmlfile = File.new("movies.xml")
Document.parse_stream(xmlfile, list)

```

---

## XPath 和 Ruby

- XPath即为XML路径语言，它是一种用来确定XML（标准通用标记语言的子集）文档中某部分位置的语言


```ruby
#!/usr/bin/ruby -w
 
require 'rexml/document'
include REXML
 
xmlfile = File.new("movies.xml")
xmldoc = Document.new(xmlfile)
 
# 第一个电影的信息
movie = XPath.first(xmldoc, "//movie")
p movie
 
# 打印所有电影类型
XPath.each(xmldoc, "//type") { |e| puts e.text }
 
# 获取所有电影格式的类型，返回数组
names = XPath.match(xmldoc, "//format").map {|x| x.text }
p names


```
