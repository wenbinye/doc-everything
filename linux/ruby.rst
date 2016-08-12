ruby
==============================

使用淘宝源
---------------------------------

::

    $ gem sources --remove https://rubygems.org/
    $ gem sources -a https://ruby.taobao.org/"gem sources -a https://ruby.taobao.org/
    $ gem sources -l
   
RUBY_BUILD_MIRROR_URL=http://ruby.taobao.org/mirrors/ruby/2.2/ruby-2.2.2.tar.gz rbenv install 2.2.2

安装 rbenv
------------------------------

git clone https://github.com/sstephenson/rbenv.git  ~/.rbenv

gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/

Programming Ruby
==============================

rdoc 提取源代码中的注释，ri 查看文档

面向对象 ::

    class Song
      def initialize(name)
        @name = name
      end
    end

    song1 = Song.new("Ruby Tuesday")

继承 ::

   class KaraokSong < Song

类方法 ::

   attr_reader :name
   attr_writer :name

单例 ::

   class MyLogger
       private_class_method :new
       @@instance = nil
       def MyLogger.create
          @@instance = new unless @@instance
          @@instance
       end
   end

`#{expr}` 表达式内插

缩进不重要，结束使用 end

方法 return 可以忽略

命名规则：

* 局部变量，方法参数，方法名使用小写字母或下划线开始。
* 全局变量使用 $ 前缀。
* 实例变量使用 @ 前缀。
* 类变量使用 @@ 前缀。
* 类名，模块名，常量都使用大写字母开始。

IO 函数：
* puts
* print
* printf
* gets
  
container 方法：

a.class
a.length

字符串操作
------------------------------

String#split
String#chomp
