# **Ruby** 信号


---

## 许多操作系统都允许将信号发送到正在运行的进程。一些信号对过程有明确的影响，而另一些则可能被困在代码层面并采取行动
---

## demo


```ruby
loop do
  sleep 1
  Signal.trap("TERM") do
    puts "exitasdas"
    exit
  end
end

# kill -15 捕获,执行退出
```

