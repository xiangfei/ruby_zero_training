# **Ruby** on Rails


---

## 什么是rails

- ruby web mvc框架
- Convention Over Configuration
- Don't Repeat Yourself
---


---

## 创建rails 项目

---

- 安装 rails

```
gem install rails

```
- 创建项目

```
rails new blog

```


---

## 启动rails

```
cd rails_project

rails server
```

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

