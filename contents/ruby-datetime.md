# ruby **日期 & 时间**

---
## Time 

Time类在 Ruby 中用于表示日期和时间。它是基于操作系统提供的系统日期和时间之上。该类可能无法表示 1970 年之前或者 2038 年之后的日期。

---
## 创建当前的日期和时间

```ruby
#!/usr/bin/ruby -w
# -*- coding: UTF-8 -*-

time1 = Time.new

puts "当前时间 : " + time1.inspect

# Time.now 功能相同
time2 = Time.now
puts "当前时间 : " + time2.inspect

```

<div class="fragment fade-in-then-out">
  <pre>
    <code class="hljs" data-trim data-line-numbers="4,8-11">

当前时间 : 2019-09-20 15:25:19 +0800
当前时间 : 2019-09-20 15:25:20 +0800

    </code>
  </pre>

</div>

---

## 获取 Date & Time 组件

- 我们可以使用 Time 对象来获取各种日期和时间的组件。请看下面的实例：

```ruby
time = Time.new

# Time 的组件
puts "当前时间 : " + time.inspect
puts time.year    # => 日期的年份
puts time.month   # => 日期的月份（1 到 12）
puts time.day     # => 一个月中的第几天（1 到 31）
puts time.wday    # => 一周中的星期几（0 是星期日）
puts time.yday    # => 365：一年中的第几天
puts time.hour    # => 23：24 小时制
puts time.min     # => 59
puts time.sec     # => 59
puts time.usec    # => 999999：微秒
puts time.zone    # => "UTC"：时区名称

```


---

## 时区和夏令时

```ruby
time = Time.new

# 这里是解释
time.zone       # => "UTC"：返回时区
time.utc_offset # => 0：UTC 是相对于 UTC 的 0 秒偏移
time.zone       # => "PST"（或其他时区）
time.isdst      # => false：如果 UTC 没有 DST（夏令时）
time.utc?       # => true：如果在 UTC 时区
time.localtime  # 转换为本地时区
time.gmtime     # 转换回 UTC
time.getlocal   # 返回本地区中的一个新的 Time 对象
time.getutc     # 返回 UTC 中的一个新的 Time 对象
```
---

## 格式化时间和日期

```ruby
time = Time.new
puts time.to_s
puts time.ctime
puts time.localtime
puts time.strftime("%Y-%m-%d %H:%M:%S")

```

---

## 时间格式化指令

|指令 | 描述|
|:--:|:--:|
|%Y |带有世纪的年份
|%y |不带世纪的年份表示（00 到 99）。
|%H	|一天中的第几小时，24 小时制（00 到 23）。
|%d	|一个月中的第几天（01 到 31）
|%m	|一年中的第几月（01 到 12）。
|%M	|小时中的第几分钟（00 到 59）。
|%S|分钟中的第几秒（00 或 60）。

---

## Time.utc、Time.gm 和 Time.local 函数
- 这些函数可用于格式化标准格式的日期

```ruby
# July 8, 2008
Time.local(2008, 7, 8)  
# July 8, 2008, 09:10am，本地时间
Time.local(2008, 7, 8, 9, 10)   
# July 8, 2008, 09:10 UTC
Time.utc(2008, 7, 8, 9, 10)  
# July 8, 2008, 09:10:11 GMT （与 UTC 相同）
Time.gm(2008, 7, 8, 9, 10, 11)  
```

---
## 时间算法

```
now = Time.now           # 当前时间
puts now

past = now - 10          # 10 秒之前。Time - number => Time
puts past

future = now + 10        # 从现在开始 10 秒之后。Time + number => Time
puts future

diff = future - now      # => 10  Time - Time => 秒数
puts diff
```


