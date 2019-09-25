# **Ruby** bundle


---

## bundle 作用

- 加载ruby启动的类库
- 解决类库冲突

---

## bundle 安装


```ruby
gem install bundle

```
---


## Gemfile定义


```

source 'http://gems.ruby-china.com'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.4.2'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 5.2.3'
# Use mysql as the database for Active Record
gem 'mysql2', '>= 0.4.4', '< 0.6.0'
# Use Puma as the app server
gem 'puma', '~> 3.11'
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
# gem 'jbuilder', '~> 2.5'
# Use Redis adapter to run Action Cable in production
# gem 'redis', '~> 4.0'
# Use ActiveModel has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use ActiveStorage variant
# gem 'mini_magick', '~> 4.8'

# Use Capistrano for deployment
# gem 'capistrano-rails', group: :development

# Reduces boot times through caching; required in config/boot.rb
gem 'bootsnap', '>= 1.1.0', require: false

# Use Rack CORS for handling Cross-Origin Resource Sharing (CORS), making cross-origin AJAX possible
gem 'rack-cors'

gem 'kaminari' , '1.1.1'
#gem 'api-pagination', '4.8.2'

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

group :development do
  gem 'awesome_print'
  gem 'listen', '>= 3.0.5', '< 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

# oauth ,外部认证接口
gem 'omniauth-ldap' , '2.0.0'

# http post gem
gem 'faraday' , '0.15.4'
gem 'faraday_middleware' , '0.13.1'

#pdf plugin
gem "prawn" , "2.2.2"
gem "prawn-table" , "0.2.2"

#excel plugin

#gem "rubyzip", ">= 1.2.1"
# gem "axlsx", git: "https://github.com/randym/axlsx.git", ref: "c8ac844"

gem "axlsx" , "2.0.1"

# ssh client
gem "net-ssh", "5.0.2"
#ftp client
gem "net-sftp", "2.1.2"
#openstack
gem "fog-openstack" , "1.0.8"
#line color
gem "rainbow"
gem "redis", "~> 4.0"

gem "sidekiq", "~> 5.1", ">= 5.1.3"
gem "sidekiq-scheduler", "~> 3.0"
gem "sidekiq-cron", "~> 1.1"

gem 'redis-rails'
# 管理rails配置文件
gem 'dotenv-rails'
gem "sidekiq-status"
gem 'ruby-jmeter'
gem 'acts_as_tree'
#gem 'ancestry'
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

```

---

## lock file 作用

- gem 文件更新报错

---

## 安装gem file

```ruby
bundle  install 

```

---

## 查看引用哪些gem文件

```ruby

bundle list

```

---

## 查看gem 安装路径


```
bundle info gem_file
```

---

##  执行脚本

- 需要Gemfile 在同意目录

```ruby

bundle exec ruby a.rb 

```







