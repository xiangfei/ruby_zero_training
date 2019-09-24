# **Ruby** 多进程


---
## 多进程
- 进程间无法共享内存数据进行读写
- 2.0 开始 Copy On Write 功能可以让 fork 的进程共享内存数据，只在数据修改时才会复制数据
- 每个进程可以运行于不同的 CPU 核心上，更充分的利用多核 CPU
- 进程间的数据隔离的同时也提高了安全性，避免了像多线程间数据错乱的风险
- 同样由于进程间的数据隔离，在进程间的通信相对来说更加困难

---

## 创建进程

```ruby

pid = fork do

end
```


---

## process detach

- 防止产生僵尸进程

---
## process wait2

- 等待子进程完成

---

## 进程数据共享

- pipeline
- socket
- process wait
---

## pipeline

```ruby
reader, writer = IO.pipe

fork do
  reader.close
  
  10.times do
    # heavy lifting
    writer.puts "Another one bites the dust"
  end
end

writer.close
while message = reader.gets
  $stdout.puts message
end

```

---

## socket

<aside class="notes">
  创建一对socket, connect to each other

</aside>

```ruby
require 'socket'

child_socket, parent_socket = Socket.pair(:UNIX, :DGRAM, 0)
maxlen = 1000

fork do
  parent_socket.close
  
  10.times do
    instruction = child_socket.recv(maxlen)
    child_socket.send("#{instruction} accomplished!", 0)
  end 
end 
child_socket.close

5.times do
  parent_socket.send("Heavy lifting", 0)
end 
5.times do
  parent_socket.send("Feather lifting", 0)
end 

10.times do
  $stdout.puts parent_socket.recv(maxlen)
end 

```

---

## process wait

<aside class="notes">
  
One problem is you need to use Process.wait to wait for your forked processes to complete. The other is that you can't do interprocess communication through variables

</aside>

```ruby
@one = nil
@two = nil
@hash = {}
pidA = fork do
    sleep 1
    @one = 1
    @hash[:one] = 1
    p [:one, @one, :hash, @hash] #=> [ :one, 1, :hash, { :one => 1 } ]
end
pidB = fork do
    sleep 2
    @two = 2
    @hash[:two] = 2
    p [:two, @two, :hash, @hash] #=> [ :two, 2, :hash, { :two => 2 } ]
end
Process.wait(pidB)
Process.wait(pidA)
p [:one, @one, :two, @two, :hash, @hash] #=> [ :one, nil, :two, nil, :hash, {} ]

```


