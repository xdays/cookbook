# variable

## scop

```
$x = 0
x = 0

require "./sub"

p $x   #=> 1
p x    #=> 0 
```

sub.rb

```
$x = 1  ## 对全局变量赋值
x = 1   ## 对局部变量赋值 
```

## asignment

```
a, b, c, d = 1, 2
a, b, c, d = 1, 2
a, b, * c = 1, 2, 3, 4, 5
a, * b, c = 1, 2, 3, 4, 5
```

# condition control

```
a = 10
b = 20
if a > b
  puts "a 比b 大"
elsif a < b
  puts "a 比b 小"
else
  puts "a 与b 相等"
end 
```

```
a = 10
b = 20
unless a > b
  puts "a 不比b 大"
en 
```

```
tags = [ "A", "IMG", "PRE" ]
tags.each do |tagname|
  case tagname
  when "P","A","I","B","BLOCKQUOTE"
    puts "#{tagname} has child."
  when "IMG", "BR"
    puts "#{tagname} has no child."
  else
    puts "#{tagname} cannot be used."
  end
end 
```

# loop

```
5.times do |i|
  puts i
end
```

```
sum = 0
for i in 1..5
  sum = sum + i
end
puts sum 

names = ["awk", "Perl", "Python", "Ruby"]
for name in names
  puts name
end
```

```
sum = 0
i = 1
while i <= 5
  sum += i
  i += 1
end
puts sum
```

```
names = ["awk","Perl","Python","Ruby"]
names.each do |name|
  puts name
end 
```

```
loop do
  print "Ruby!"
end
```


```
puts "break 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    break
  end
  p [i,lang]
end

puts "next 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    next
  end
  p [i,lang]
end

puts "redo 的例子:"
i = 0
["Perl", "Python", "Ruby", "Scheme"].each do |lang|
  i += 1
  if i == 3
    redo
  end
  p [i,lang]
end
```

# method

```
def hello(name="Ruby")
  puts "Hello, #{name}."
end

hello("Ruby")
```

```
def foo(*args)
  args
end

p foo(1, 2, 3)    #=> [1, 2, 3] 
```

```
def meth(x: 0, y: 0, z: 0, **args)
  [x, y, z, args]
end

p meth(z: 4, y: 3, x: 2)        #=> [2, 3, 4, {}]
p meth(x: 2, z: 3, v: 4, w: 5)  #=> [2, 0, 3, {:v=>4, :w=>5}]
```

# class and module

```
class HelloWorld                   # class 关键字
  def initialize(myname = "Ruby")  # initialize 方法
    @name = myname # 初始化实例变量
  end

  def hello                        # 实例方法
    puts "Hello, world. I am       #{@name}."
  end
end

bob = HelloWorld.new("Bob")
alice = HelloWorld.new("Alice")
ruby = HelloWorld.new

bob.hello 
```

```
class HelloWorld
  attr_accessor :name
end 
```

```
class << HelloWorld
  def hello(name)
    puts "#{name} said hello."
  end
end

HelloWorld.hello("John")    #=> John said hello.

class HelloWorld
  class << self
    def hello(name)
      puts "#{name} said hello."
    end
  end
end 

def HelloWorld.hello(name)
  puts "#{name} said hello."
end

HelloWorld.hello("John")    #=> John said hello. 
```

```
class AccTest
  def pub
    puts "pub is a public method."
  end

  public :pub   # 把pub 方法设定为public（可省略）

  def priv
    puts "priv is a private method."
  end

  private :priv # 把priv 方法设定为private
end
```

# error and exception

```
ltotal=0                             # 行数合计
wtotal=0                             # 单词数合计
ctotal=0                             # 字数合计
ARGV.each do |file|
  begin
    input = File.open(file)          # 打开文件（A）
    l=0                              # file 内的行数
    w=0                              # file 内的单词数
    c=0                              # file 内的字数
    input.each_line do |line|
      l += 1
      c += line.size
      line.sub!(/^\s+/, "")          # 删除行首的空白符
      ary = line.split(/\s+/)        # 用空白符分解
      w += ary.size
    end
    input.close                      # 关闭文件
    printf("%8d %8d %8d %s\n", l, w, c, file)  # 整理输出格式
    ltotal += l
    wtotal += w
    ctotal += c
  rescue => ex
    print ex.message, "\n"           # 输出异常信息（B）
    end
end

printf("%8d %8d %8d %s\n", ltotal, wtotal, ctotal, "total")
```

# block

## block usage

```
file = File.open("sample.txt")
file.each_line do |line|
  print line
end
file.close 
```

```
File.open("sample.txt") do |file|
  file.each_line do |line|
    print line
  end
end 
```

```
array = ["ruby", "Perl", "PHP", "Python"]
sorted = array.sort{ |a, b| a.length <=> b.length }
p sorted    #=> ["PHP", "ruby", "Perl", "Python"]
```

## define block method 

```
def myloop
  while true
    yield               # 执行块
  end
end

num = 1                 # 初始化num
myloop do
  puts "num is #{num}"  # 输出num
  break if num > 100    # num 超过100 后跳出循环
  num *= 2              # num 乘2
end 
```

```
def total(from, to)
  result = 0                # 合计值
  from.upto(to) do |num|    # 处理从from 到to 的值
    if block_given?         #   如果有块的话
      result += yield(num)  #     累加经过块处理的值
    else                    #   如果没有块的话
      result += num         #     直接累加
    end
  end
  return result             # 返回方法的结果
end

p total(1, 10)                  # 从1 到10 的和 => 55
p total(1, 10){|num| num ** 2 } # 从1 到10 的2 次幂的和 => 385 
```

## block as object

```
def total2(from, to, &block)
  result = 0               # 合计值
  from.upto(to) do |num|   # 处理从from 到to 的值
    if block               #   如果有块的话
      result +=            #     累加经过块处理的值
           block.call(num)
    else                   #   如果没有块的话
      result += num        #     直接累加
    end
  end
  return result            # 返回方法的结果
end

p total2(1, 10)                   # 从1 到10 的和 => 55
p total2(1, 10){|num| num ** 2 }  # 从1 到10 的2 次幂的和 => 385
```

```
def call_each(ary, &block)
  ary.each(&block)
end

call_each [1, 2, 3] do |item|
  p item
end
```

## block variable

```
x = 1            # 初始化x
y = 1            # 初始化y
ary = [1, 2, 3]

ary.each do |x|  # 将x 作为块变量使用
  y = x          # 将x 赋值给y
end

p [x, y]         # 确认x 与y 的值 
```

```
x = y = z = 0       # 初始化x、y、z
ary = [1, 2, 3]
ary.each do |x; y|  # 使用块变量x，块局部变量y
  y = x             # 代入块局部变量y
  z = x             # 代入不是块局部变量的变量z
  p [x, y, z]       # 确认块内的 x、y、z 的值
end
puts
p [x, y, z]         # 确认x、y、z 的值
```
