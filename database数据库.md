# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [mysql](#mysql)
   * [sqlite](#sqlite)

<!-- Added by: luyl, at: 2019-01-29T10:20+08:00 -->

<!--te-->

----

# mysql

* [21分钟 MySQL 入门教程](https://www.cnblogs.com/mr-wid/archive/2013/05/09/3068229.html)

```
登录：
	mysql -u root -p

查看版本
    1) 终端   mysql -V
    2) mysql中：status;
    3) 使用mysql的函数 select version();

1.选择
    1) 查看所有数据库：show databases；
    2) 选择数据库：use <dataname>；
    3) 显示数据库中所有表：show tables；
    4) 显示表中所有字段：desc <tablename>；
    5) 显示表中所有内容：select * from <tablename>；
 
2.创建数据库
    create database <database_name>；

3.添加，修改
    1) 添加一个字段   
        ALTER TABLE jw_user_role ADD zk_env VARCHAR(16);  
    2) 修改字段为not null，还要把原来的类型也写出来
        ALTER TABLE jw_user_role MODIFY  zk_env VARCHAR(16) NOT NULL;  
        字段属性为not null,改为null
        ALTER TABLE 表名 CHANGE 原字段名称 新字段名称 数据类型 NULL;
    3) 添加一个非空字段
        ALTER TABLE books_author ADD COLUMN sex VARCHAR(1);【先创建NULL型字段】
        UPDATA books_author SET sex='M'; 【再将该字段的值填充为某个默认值】
        ALTER TABLE books_author MODIFY sex VARCHAR(1) NOT NULL; 【最后将该字段改为NOT NULL型】
    4) 更改列名
        ALTER TABLE student CHANGE physics physisc CHAR(10) NOT NULL; 

4.删除
    1) 删除表：drop table <tablename>；
    2) 删除数据库：drop database <databsename>;
    3) 清空表中数据：delete from <tablename>; 或者 truncate table <tablename>; 
    效率上truncate比delete快，但truncate删除后不记录mysql日志，不可以恢复数据。
    delete的效果有点像将mysql表中所有记录一条一条删除到删完，
    而truncate相当于保留mysql表的结构，重新创建了这个表，所有的状态都相当于新表。
```

5.常见错误
	1) ERROR 1701 (42000): Cannot truncate a table referenced in a foreign key constraint 

	执行以下语句可以执行成功:

	SET FOREIGN_KEY_CHECKS=0;

	TRUNCATE TABLE tableName;

	SET FOREIGN_KEY_CHECKS=1;

----

# sqlite

* [使用SQLite-廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001388320596292f925f46d56ef4c80a1c9d8e47e2d5711000)


**基本操作**

SQLite是一种嵌入式数据库，它的数据库就是一个文件。由于SQLite本身是C写的，而且体积很小，所以，经常被集成到各种应用程序中，
甚至在iOS和Android的App中都可以集成。

Python就内置了SQLite3，所以，在Python中使用SQLite，不需要安装任何东西，直接使用。

在使用SQLite前，我们先要搞清楚几个概念：

表是数据库中存放关系数据的集合，一个数据库里面通常都包含多个表，比如学生的表，班级的表，学校的表，等等。表和表之间通过外键关联。

要操作关系数据库，首先需要连接到数据库，一个数据库连接称为Connection；

连接到数据库后，需要打开游标，称之为Cursor，通过Cursor执行SQL语句，然后，获得执行结果。

Python定义了一套操作数据库的API接口，任何数据库要连接到Python，只需要提供符合Python标准的数据库驱动即可。

由于SQLite的驱动内置在Python标准库中，所以我们可以直接来操作SQLite数据库。

我们在Python交互式命令行实践一下：

```
# 导入SQLite驱动:
>>> import sqlite3
# 连接到SQLite数据库
# 数据库文件是test.db
# 如果文件不存在，会自动在当前目录创建:
>>> conn = sqlite3.connect('test.db')
# 创建一个Cursor:
>>> cursor = conn.cursor()
# 执行一条SQL语句，创建user表:
>>> cursor.execute('create table user (id varchar(20) primary key, name varchar(20))')
<sqlite3.Cursor object at 0x10f8aa260>
# 继续执行一条SQL语句，插入一条记录:
>>> cursor.execute('insert into user (id, name) values (\'1\', \'Michael\')')
<sqlite3.Cursor object at 0x10f8aa260>
# 通过rowcount获得插入的行数:
>>> cursor.rowcount
1
# 关闭Cursor:
>>> cursor.close()
# 提交事务:
>>> conn.commit()
# 关闭Connection:
>>> conn.close()
```

我们再试试查询记录：

```
>>> conn = sqlite3.connect('test.db')
>>> cursor = conn.cursor()
# 执行查询语句:
>>> cursor.execute('select * from user where id=?', ('1',))
<sqlite3.Cursor object at 0x10f8aa340>
# 获得查询结果集:
>>> values = cursor.fetchall()
>>> values
[(u'1', u'Michael')]
>>> cursor.close()
>>> conn.close()
```

使用Python的DB-API时，只要搞清楚Connection和Cursor对象，打开后一定记得关闭，就可以放心地使用。

使用Cursor对象执行`insert`，`update`，`delete`语句时，执行结果由rowcount返回影响的行数，就可以拿到执行结果。

使用Cursor对象执行`select`语句时，通过`featchall()`可以拿到结果集。结果集是一个list，每个元素都是一个tuple，对应一行记录。

如果SQL语句带有参数，那么需要把参数按照位置传递给`execute()`方法，有几个`?`占位符就必须对应几个参数，例如：

```
cursor.execute('select * from user where name=? and pwd=?', ('abc', '123456'))
```

SQLite支持常见的标准SQL语句以及几种常见的数据类型。具体文档请参阅SQLite官方网站。


**小结**

在Python中操作数据库时，要先导入数据库对应的驱动，然后，通过Connection对象和Cursor对象操作数据。

要确保打开的Connection对象和Cursor对象都正确地被关闭，否则，资源就会泄露。

如何才能确保出错的情况下也关闭掉Connection对象和Cursor对象呢？请回忆`try:...except:...finally:...`的用法。

**常见问题**

1. 查看数据库中所有表

	[xbl1986的专栏](http://blog.csdn.net/xbl1986/article/details/7440029)

	SQL的语句是

	```
	select name from sqlite_master where type = 'table' order by name
	```

	放到python里就需要变成

	```
	print cur.execute("select name from sqlite_master where type = 'table' order by name").fetchall()
	```

	这样打印出来的就是`[(u'table_name',)]`

	而用

	```
	cur.execute("select * from sqlite_master").fetchall()
	```

	的话，则打印出来更多的信息，虽然现在还不知道格式是怎么回事吧

2. 判断指定表是否存在

	```
	select count(*)  from sqlite_master where type='table' and name = 'yourtablename';
	```

	其中yourtablename表示你要判断的表名，如果结果大于0，表示改表存在数据库中，否则不存在。

3. 查询表中的所有字段信息

	```
	PRAGMA table_info([tablename])
	```

	比如：我想看看出表tbl_sfg_device表的所有列信息，可以用下述代码：

	```
	PRAGMA table_info(tbl_sfg_device)
	```

	注意： `PRAGMA`必须大写

4. 查看表中共有多少条记录

	```
	select count(*)  from table_name
	```