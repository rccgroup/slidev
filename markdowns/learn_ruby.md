---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# colorSchema: 'dark'
# some information about the slides, markdown enabled
info: |
  ## Ruby 培训资料

---

# Ruby 培训资料

FROM RCC

---

## 一、工具与调试

1、RVM

RVM 是一个命令行工具，可以提供一个便捷的多版本 Ruby 环境的管理和切换。

官方网站：https://rvm.io/

常用的命令：

```bash
# 列出已知的 Ruby 版本
rvm list known

# 安装一个 Ruby 版本 (--disable-binary)
rvm install ruby-2.6.3

# 切换 Ruby 版本 (设置为默认版本: --default)
rvm use ruby-2.6.3

# 删除 Ruby 版本
rvm remove ruby-2.6.3
```

---

2、irb

`irb` 是 `Ruby` 附带的交互式编程环境。

只需要一个命令，就可以进入到ruby环境，运行你的代码。

```bash
# 终端输入 irb 进入

irb(main):001:0> 23 + 27
=> 50

irb(main):008:0> hi = "Hello, Rcc!"
=> "Hello, Rcc!"

....
```

输入 `exit` 或 `quit` 退出`irb` 。

---

3、断点

相信你以前写代码的时候，也经常使用到断点，不得不说断点真的是我们程序员写代码的“必备良药”。

Gemfile 安装 gem

```ruby
gem "pry-byebug", "~> 3.8.0"
```

执行：`bundle install` 进行安装。

然后在需要调试的地方加入一行：

```ruby
binding.pry
```

常用操作步骤：

```bash
next
step
quit
```

---

## 二、常见的数据类型

ruby中的数据类型与其他语言还是有很多共通的地方的~

---

## 三、流程控制

待写

---

## 四、类、实例变量、实例方法、类方法

1、在 Ruby 中，可以用 class 定义一个类。类名的首字母应该**大写**。

```ruby
class Customer
end
```

2、用 new 生成类的实例。

```ruby
customer1 = Customer.new
customer2 = Customer.new
```

---

3、为类定义一个实例方法。

```ruby
class Customer
  def hello
    puts "Hello Ruby!"
  end
end

customer1 = Customer.new
customer1.hello
```

4、定义一个类方法。

```ruby
class Customer
   def self.world
    puts "world ruby!"
   end
end

# 类方法的调用
Customer.world
```

---

5、实例变量

- 以“@”符号开头。
- 实例变量属于该实例方法所在类的实例，而不是属于该方法。
- 所以实例变量，在实例方法里面都可以访问到。
- 实例变量无须显式声明即可使用。如果使用一个未定义的实例变量，则该实例变量的值为nil。

```ruby
class Customer
  def info1
    p @name
  end

  def info2
    @name = 'customer'
  end

end

customer = Customer.new

customer.info1
customer.info2
customer.info1

```

---

6、使用 initialize 初始化实例变量：

```ruby
class Customer
   def initialize(id, name, addr)
      @cust_id = id
      @cust_name = name
      @cust_addr = addr
   end

   def show
     "id: #{@cust_id}, name: #{@cust_name}, addr: #{@cust_addr}"
   end
end

cust1 = Customer.new("1", "John", "Wisdom Apartments, Ludhiya")
cust2 = Customer.new("2", "Poul", "New Empire road, Khandala")

cust1.show
cust2.show
```

<br>
<br>

> 自行了解：
> - attr_accessor


---

## 二、打开类、猴子补丁

1、打开类

<div class="grid grid-cols-2 gap-x-4">
<div>

先看个例子。

```ruby
class D
  def x; 'x'; end
end

class D
  def y; 'y'; end
end

obj = D.new
obj.x   # => "x"
obj.y   # => "y"
```

</div>

<div>

上面包含了两个地方 `class D` 的定义，但是不会出现2个类的定义。

也就是说，在第二次定义 D 类时，Ruby 能够找到第一次定义的 D 类并把新的方法（y）添加到 D 类中。

这叫做 “打开类” (Open class)。

> 换句话说，可以在任何时候打开一个已经存在的类，并向里面添加新的方法——包括 String 和 Array 这样的标准类。

</div>
</div>

---

2、猴子补丁

当打开类重新定义新的方法时，如果跟该类已有的方法重名，原来的方法就会被覆盖。

这称之为「猴子补丁（MonkeyPatch）」。

<div class="grid grid-cols-2 gap-x-4">
<div>

举个例子，你打开 String 类，并添加一个实例方法

```ruby
class String
  def myself_to_s
    "myself to_s"
  end
end
```

这个时候，你发现名字太长了，灵机一动把名字改成了 to_s

```ruby
class String
  def to_s
    "myself to_s"
  end
end
```

</div>

<div>

从这个案例其实可以知道：

- Ruby可以很方便地打开一个已定义的类，重载里面已有的方法
- 猴子补丁有时是危险的

</div>
</div>

---

## 三、模块

1、模块可以将方法，类和常量组合在一起


<div class="grid grid-cols-2 gap-x-4">
<div>

定义一个模块：

```ruby
module Trig
   PI = 3.141592654

   def sin
     puts 'sin'
   end

   def cos
     puts 'cos'
   end
end

Trig::PI

```

</div>

<div>

模块有两个主要好处：

- 模块提供名称空间并防止名称冲突。
- 模块实现了mixin 功能。

<br>
<br>
<br>

> 需要注意：
> 模块并不能生成实例。比如 Trig.new 。

</div>
</div>

---

2、include

当类 include 模块之后，就相当于给类添加了「实例方法」。

```ruby
class Sample
  include Trig
end

Sample.new.sin
```

3、extend

当类 extend 模块以后，就相当于给类添加了「类方法」。

```ruby
class Sample
  extend Trig
end

Sample.sin
```

这种  `include / extend` 的能力，被称为 `mixin`  。

可以将方法按模块组织，然后被各个其他类引用，达到复用的效果。

---

## 五、特性

1、迭代器

其他语言中，进行遍历，可能更多是使用 `for / while` 循环来处理。

而在 Ruby 中，更多是使用 迭代器 来进行相关的处理。

- 打印出数组的每个元素 — — `each`

<div class="grid grid-cols-2 gap-x-4">
<div>

```ruby
# 定义一个数组
users = ['oliver', 'peter', 'xiaoming', 'cc']

# 多行
users.each do |username|
  puts username
end

# oliver
# peter
# xiaoming
# cc

# 单行
users.each { |username| puts username }
```

</div>

<div>

```ruby
# 如果需要带上索引, 使用 each_with_index，注意参数由1个变成2个
users.each_with_index do |username, index|
  puts "index: #{index}, #{username}"
end

# index: 0, oliver
# index: 1, peter
# index: 2, xiaoming
# index: 3, cc
```

</div>
</div>
---

- 将每个元素的处理结果返回 — — `map`

```ruby
# 定义一个数组
users = ['oliver', 'peter', 'xiaoming', 'cc']

users.map { |username| username.upcase }

# ["OLIVER", "PETER", "XIAOMING", "CC"]
```

<br>

- 进行过滤，返回条件为 true 的元素 — —  `select`

```ruby
users = ['oliver', 'peter', 'xiaoming', 'cc']

users.select { |username| username == 'xiaoming' }
# ["xiaoming"]
```

<br>

- 所有元素都满足条件，返回 true / false — —  `all?`

```ruby
numbers = [1, 2, 3, 4]

numbers.all? { |num| num > 0 }
```

---

- 所有元素中有任意一个满足条件即可， 返回 true / false  — — `any?`

```ruby
numbers = [1, 2, 3, 4]

numbers.any? { |num| num > 0 }
```

<br>

- 进行次数循环 — —  `times`

```ruby
10.times { |i| puts i }
```

<br>
<br>

看了以上的例子，可以发现，对于这种遍历元素，针对元素进行不同处理的形式，

在 Ruby 中，都是`迭代 + 块`方式来处理。

相关的方法有很多，可以查阅文档，包括 Hash / Array / … 。[Array](https://apidock.com/ruby/Array)

---

2、block — — 块

我们上面看到的多行 `do |xx| … end` 结构，或者单行 `{  |xx|  … }`  格式，就是一个块。

- 怎么定义一个块？
- 一个块可以用来干嘛？

<div class="grid grid-cols-2 gap-x-4">
<div>

在定义一个方法的时候：

```ruby
def say_hello
  yield  # 表示接收一个 block
end

# 进行方法调用，可以传入一个 block
say_hello do
  puts 'block - 1 do.'
end

say_hello do
  puts 'block - 2 do.'
end
```

</div>

<div>

另一种格式：

```ruby
# &block 表示接收一个块
def say_hello_other(&block)
  # 判断是否有传入 block，有传入的话再进行 block 的调用
  if block_given?
    block.call
  end
end

say_hello_other { puts 'block - other do.' }
```

</div>
</div>

---

那么可以看到，基于这种模式，像上面迭代器中的各种方法的实现，

其实都是在调用的传入一个 `block`，在 `block` 做各种不同的处理。

- [Understanding Ruby Blocks.](https://medium.com/@noordean/understanding-ruby-blocks-3a45d16891f1)
- [Mastering Ruby Blocks in Less Than 5 Minutes](https://mixandgo.com/learn/ruby-blocks)

---

3、当前对象（self）

- 在 Ruby 中，`self` 是一个特殊的变量，它指向当前的对象。
- 它也是默认方法接收者。
- 实例变量就是在 `self` 中查找的。

<div class="grid grid-cols-2 gap-x-4">
<div>

```ruby
class User
  def initialize(name)
    @name = name
  end

  def say
    puts "通用实例方法"

    # 调用另一个实例方法
    self.email_noti

    puts self
  end

  def email_noti
    puts 'email_noti'
  end
end
```

</div>

<div>

```ruby
user = User.new("xiaoming")

user.say
# "通用实例方法"
# "email_noti"
# #<User:0x00007ffb8e11e018 @name="xiaoming">
```

</div>
</div>

---

<div class="grid grid-cols-2 gap-x-4">
<div>

```ruby
class User
  # 类方法
  # 注意：当前 self 是指？打开当前类，当前作用域下，就是 User。
  def self.all_can_use
   puts '使用 User.all_can_use 进行调用'
  end

  # 类方法的另一种写法
  # 使用 `class << `, 表示打开某个对象，添加属于它自己的方法
  # class << self 或者 class << User
  class << self
   def all_can_use_2
     puts '使用 User.all_can_use_2 进行调用'
   end
  end
end
```

</div>

<div>

```ruby
User.all_can_use
# 使用 User.all_can_use 进行调用

User.all_can_use_2
# 使用 User.all_can_use_2 进行调用
```

</div>
</div>

在 Ruby 中，需要时刻注意当前的 `self` 是谁。
理解了 当前的`self`，很多问题都会变得清晰。

---

## 六、对象模型

1、继承链

```ruby
class User
  def initialize(name)
    @name = name
  end
end

user = User.new("xiaoming")

# 查看 user 的类
user.class  # User

# 查看 User 类的超类
user.class.superclass  # Object 。也就是表示： User 继承自 Object

# 查看祖先链（类的祖先链）
user.class.ancestors
# [User, Object, Kernel, BasicObject]
```

祖先链由类和其超类以及module组成。

---

2、方法查找

<div class="grid grid-cols-2 gap-x-4">
<div>

```ruby
class User
  def initialize(name)
    @name = name
  end

  def say
    "通用实例方法"
  end
end

user = User.new("xiaoming")
user_2 = User.new("cc")

# 单独給一个对象新增一个方法
def user.my_posts
  ["文章1", "文章2"]
end
```

</div>

<div>

Ruby 中，一个实例方法的查找，顺序如下：

- 先确定当前对象（`receiver`），先查找该对象是否有单独定义方法。
- 继而查找当前对象的类中定义的实例方法，并沿着祖先链往上找定义的实例方法。
- 如果找不到，会调用 `method_missing` 方法。如果 `method_missing` 没有定义，则抛出 `NoMethodError` 异常。

</div>
</div>

---

## 七、黑魔法

1、方法调用可以省略括号

```ruby
def say
  puts 'say'
end

# 调用
=> say
=> say()

---------------------

def hello(name)
  puts "hello, #{name}"
end

# 调用
=> hello "xiaoming"
=> hello("xiaoming")
```

---

2、ruby中【*】和【**】的功用

<div class="grid grid-cols-2 gap-x-4">
<div>

- 用 ` *args ` 的形式来接收不确定个数的参数。

```ruby
def splat_arguments(*args)
  args
end

splat_arguments(:linux, "ms")
# => [:linux, "ms"]

splat_arguments(:linux, "ms", String)
# => [:linux, "ms", String]

```

</div>

<div>

-  用 ` *args ` 的形式来表示 Keyword Arguments

```ruby
def splat_arguments(*args, **keyword_args)
  p args
  p keyword_args
end

splat_arguments("first", "second", name: nil, color: 'Red')
# ["first", "second"]
# {:name=>nil, :color=>"Red"}
```

</div>
</div>

扩展阅读:

- [Everything you should know about Ruby Splats | Alex Castaño](https://alexcastano.com/everything-about-ruby-splats/)
- [Ruby: Using the Double Splat (**) with Keyword Arguments | Mike Rogers](https://mikerogers.io/2020/08/17/ruby-using-the-double-splat-with-keyword-arguments)
- [Fun with keyword arguments, hashes, and splats - Justin Weiss](https://www.justinweiss.com/articles/fun-with-keyword-arguments/)

---

3、return的规则

我们知道，在ruby中，永远是怎么方便怎么来~

那么能省略的，当然是要省略的！

```ruby
# 定义一个方法，返回结果
def add(a, b)
  return a + b
end

# 当最后一行是你的返回结果的时候，
# 则return关键字可以省略！
def add(a, b)
  a + b
end

# 需要注意的是：
# 如果不是最后一行，则return还是得乖乖地写哦~
def add(a, b)
  return 0 if b == 1

  a + b
end
```

---

4、Hash的省略

当方法的参数要求传入一个Hash的时候，则传入hash的时候，可以省略花括号：

```ruby
#原本定义一个方法，需要返回result
def func(options = {})
  options
end

#调用的时候直接省略花括号
func(a: 1, b: 2)
```

---

5、方法名带有 ！和 ?

原来ruby讲究见名知意！而且甚至要带上语气！

- "?": 表示方法返回 bool 的意愿。如 `Array.empty?` (判断数组中元素是否为空)。
- "!": 表明使用该方法时需注意，可能会改变到原有对象意愿 / 会抛弃异常等。

例子：

```ruby
Array#empty?

Array#sort
Array#sort!

String#gsub
String#gsub!

```

<br>
<br>

> Note:
>
> 方法定义后面加上的后缀，只是约定俗成，为了方便使用的时候更加清晰其方法的意义，
>
> 可以不遵守，但是为了代码的可读性，加上符号往往让你的代码更加易读~

---

## 八、资料

书籍
- 《Ruby元编程》
- railstutorial 《Ruby on Rails教程》，安道翻译。
- 《应用Rails进行敏捷Web开发》
- 《The Ruby Way》
- 《松本行弘的程序世界》

文档
- https://ruby-doc.org/
- https://rubyapi.org/


B站的视频课
- https://www.bilibili.com/video/BV1QW411F7rh
