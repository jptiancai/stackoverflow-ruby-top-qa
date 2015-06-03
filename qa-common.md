
Ruby中如何写一个switch语句？
问题[链接](http://stackoverflow.com/questions/948135/how-can-i-write-a-switch-statement-in-ruby)

Ruby使用`case`[表达式](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_expressions.html#S5)代替

```
case a
when 1..5
  puts "It's between 1 and 5"
when 6
  puts "It's 6"
when String
  puts "You passed a string"
else
  puts "You gave me #{a} -- I have no idea what to do with that."
end
```

比较对象在when子句中对象和case子句中的值使用`===`操作符比较。也就是说，`1..5===a`和`Sting===a`,而不是`a===1..5`。
上面看到的语法是非常精致的，你可以使用范围和类，或者各种各样的东西而不仅是测试相等。


默认安装gem时，使用--no-ri --no-rdoc?
问题[链接](http://stackoverflow.com/questions/1381725/how-to-make-no-ri-no-rdoc-the-default-for-gem-install)

把下一行添加进本地`~/.gemrc`文件（位于__home__文件夹）

```
gem: --no-document
```

或者你可以添加下行到全局gemrc配置文件中。如何找到它（linux中）

```
strace gem source 2>&1 | grep gemrc
```

我如何将命令行参数传递给一个rake任务？

问题[链接](http://stackoverflow.com/questions/825748/how-do-i-pass-command-line-arguments-to-a-rake-task)

通过添加任务调用的参数标志可以在rake中定义正式的参数。例如：
```
require 'rake'

task :my_task, [:arg1, :arg2] do |t, args|
  puts "Args were: #{args}"
end

task :invoke_my_task do
  Rake.application.invoke_task("my_task[1, 2]")
end

# or if you prefer this syntax...
task :invoke_my_task_2 do
  Rake::Task[:my_task].invoke(3, 4)
end

# a task with prerequisites passes its 
# arguments to it prerequisites
task :with_prerequisite, [:arg1, :arg2] => :prerequesite_task

# to specify default values, 
# we take advantage of args being a Rake::TaskArguments object
task :with_defaults, :arg1, :arg2 do |t, args|
  args.with_defaults(:arg1 => :default_1, :arg2 => :default_2)
  puts "Args with defaults were: #{args}"
end
```

之后，命令行操作：

```
> rake my_task[1,2]
Args were: {:arg1=>"1", :arg2=>"2"}

> rake "my_task[1, 2]"
Args were: {:arg1=>"1", :arg2=>"2"}

> rake invoke_my_task
Args were: {:arg1=>"1", :arg2=>"2"}

> rake invoke_my_task_2
Args were: {:arg1=>3, :arg2=>4}

> rake with_prerequisite[5,6]
Args were: {:arg1=>"5", :arg2=>"6"}

> rake with_prerequisite_2[7,8]
Args were: {:arg1=>"7", :arg2=>"8"}

> rake with_defaults
Args with defaults were: {:arg1=>:default_1, :arg2=>:default_2}

> rake with_defaults['x','y']
Args with defaults were: {:arg1=>"x", :arg2=>"y"}
```

第二个示例仅作为演示，如果你想使用空白，引号包裹住目标名称是必须的
保证空白处分隔shell。

观察**rake.rb**中的代码，rake没有解析rake字符串来提取参数作为先决条件。
所以你不能做`task :t1=> "dep[1,2]"`。识别不同参数作为先决条件的唯一途径是在依赖人物行为中显式的调用它，比如`:invoke_my_task`和`:invoke_my_task_2`

注意一些shell（比如zsh）需要忽略方括号：`rake my_task\['arg1']\`


> 译者注，关于rake的历史，请参考[Ruby on Rails中的Rake教程(Rake如何把我灌醉!)](http://www.cnblogs.com/wangyuyu/p/3301473.html)

Ruby中检查一个值是否存在一个数组？

问题[链接](http://stackoverflow.com/questions/1986386/check-if-a-value-exists-in-an-array-in-ruby)

你可以使用`[include?](http://ruby-doc.org/core-1.9.3/Array.html#method-i-include-3F)`

```
>> ['Cat', 'Dog', 'Bird'].include? 'Dog'
=> true
```

> 下面也有回答可以用%w(Cat Dog Bird).include? 'Dog'，更加方便啊


Ruby中如何将一个字符串转换为小写或大写?

问题[链接](http://stackoverflow.com/questions/1020568/how-to-convert-a-string-to-lower-or-upper-case-in-ruby)

Ruby有很多方法改变字符串的大小写。转换成小写，使用`downcase`:

```
"hello James!".downcase    #=> "hello james!"

```

同样地，`upcase`大写每一个字母和`capitalize `大写字符串的首字母，小写剩下的字母：

```
"hello James!".upcase      #=> "HELLO JAMES!"
"hello James!".capitalize  #=> "Hello james!"
```
如果改变字符串本身，你可以加上感叹号给这些方法任意一个。

```
string = "hello James!"
string.downcase!
string   #=> "hello james!"
```
更多信息参考[String文档](http://ruby-doc.org/core-2.2.2/String.html)

Ruby调用shell命令

问题[链接](http://stackoverflow.com/questions/2232/calling-shell-commands-from-ruby)

本篇解释是基于我一个朋友的[Ruby 脚本评论](http://gist.github.com/4069)，如果你想要提高这个脚本，尽情修改链接。























