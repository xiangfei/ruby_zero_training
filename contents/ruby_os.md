# **Ruby** 系统操作

- ruby 调用系统命令的方法

---

## ``


```ruby
 `ls /root`


```

---

## system

```ruby

 system "ls -ltra"

```
---

## open3

```ruby

require 'open3'

Open3::popen3( "#{cmd}") do |std_in, std_out, std_err|
        std_out.each_line do |line|
          #puts line
          block.call line if block_given?
        end
        std_err.each_line do |line|
          result = false
          logger.error("run command  #{cmd} failed  #{line}")
          #puts line
          block.call line if block_given?
        end
      end

```

---

## IO opoen

```ruby
require 'io/console'
IO.popen(["ls", "/"], :err=>[:child, :out]) {|ls_io|
  ls_result_with_error = ls_io.read
}


f = IO.popen("uname")
p f.readlines
f.close
```








