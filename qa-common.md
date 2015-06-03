
Ruby�����дһ��switch��䣿
����[����](http://stackoverflow.com/questions/948135/how-can-i-write-a-switch-statement-in-ruby)

Rubyʹ��`case`[���ʽ](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_expressions.html#S5)����

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

�Ƚ϶�����when�Ӿ��ж����case�Ӿ��е�ֵʹ��`===`�������Ƚϡ�Ҳ����˵��`1..5===a`��`Sting===a`,������`a===1..5`��
���濴�����﷨�Ƿǳ����µģ������ʹ�÷�Χ���࣬���߸��ָ����Ķ����������ǲ�����ȡ�


Ĭ�ϰ�װgemʱ��ʹ��--no-ri --no-rdoc?
����[����](http://stackoverflow.com/questions/1381725/how-to-make-no-ri-no-rdoc-the-default-for-gem-install)

����һ����ӽ�����`~/.gemrc`�ļ���λ��__home__�ļ��У�

```
gem: --no-document
```

���������������е�ȫ��gemrc�����ļ��С�����ҵ�����linux�У�

```
strace gem source 2>&1 | grep gemrc
```

����ν������в������ݸ�һ��rake����

����[����](http://stackoverflow.com/questions/825748/how-do-i-pass-command-line-arguments-to-a-rake-task)

ͨ�����������õĲ�����־������rake�ж�����ʽ�Ĳ��������磺
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

֮�������в�����

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

�ڶ���ʾ������Ϊ��ʾ���������ʹ�ÿհף����Ű���סĿ�������Ǳ����
��֤�հ״��ָ�shell��

�۲�**rake.rb**�еĴ��룬rakeû�н���rake�ַ�������ȡ������Ϊ�Ⱦ�������
�����㲻����`task :t1=> "dep[1,2]"`��ʶ��ͬ������Ϊ�Ⱦ�������Ψһ;����������������Ϊ����ʽ�ĵ�����������`:invoke_my_task`��`:invoke_my_task_2`

ע��һЩshell������zsh����Ҫ���Է����ţ�`rake my_task\['arg1']\`


> ����ע������rake����ʷ����ο�[Ruby on Rails�е�Rake�̳�(Rake��ΰ��ҹ���!)](http://www.cnblogs.com/wangyuyu/p/3301473.html)

Ruby�м��һ��ֵ�Ƿ����һ�����飿

����[����](http://stackoverflow.com/questions/1986386/check-if-a-value-exists-in-an-array-in-ruby)

�����ʹ��`[include?](http://ruby-doc.org/core-1.9.3/Array.html#method-i-include-3F)`

```
>> ['Cat', 'Dog', 'Bird'].include? 'Dog'
=> true
```

> ����Ҳ�лش������%w(Cat Dog Bird).include? 'Dog'�����ӷ��㰡


Ruby����ν�һ���ַ���ת��ΪСд���д?

����[����](http://stackoverflow.com/questions/1020568/how-to-convert-a-string-to-lower-or-upper-case-in-ruby)

Ruby�кܶ෽���ı��ַ����Ĵ�Сд��ת����Сд��ʹ��`downcase`:

```
"hello James!".downcase    #=> "hello james!"

```

ͬ���أ�`upcase`��дÿһ����ĸ��`capitalize `��д�ַ���������ĸ��Сдʣ�µ���ĸ��

```
"hello James!".upcase      #=> "HELLO JAMES!"
"hello James!".capitalize  #=> "Hello james!"
```
����ı��ַ�����������Լ��ϸ�̾�Ÿ���Щ��������һ����

```
string = "hello James!"
string.downcase!
string   #=> "hello james!"
```
������Ϣ�ο�[String�ĵ�](http://ruby-doc.org/core-2.2.2/String.html)

Ruby����shell����

����[����](http://stackoverflow.com/questions/2232/calling-shell-commands-from-ruby)

��ƪ�����ǻ�����һ�����ѵ�[Ruby �ű�����](http://gist.github.com/4069)���������Ҫ�������ű��������޸����ӡ�























