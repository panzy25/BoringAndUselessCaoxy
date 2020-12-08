# 数据库第六次作业

<center>第三章SQL语句练习作业</center>



> written by panzy25, 18372046
>
> Typora used
>
> Based on Markdown

[TOC]

## 1. Overview

​	通过安装 SQL server 2008，并熟悉管理工具常用的工具与界面， 并构建 CAP 数据库，然后对第三章出现的例题，用 CAP 数据库进行练习、验证与结果分析。思考在练习过程中 SQL 语句语法及其使用，提高数据库系统的语言使用能力。

## 2. Document

​	我们可以把 SQL 分为两个部分:数据操作语言(DML)和数据定义 语言(DDL)。SQL(结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。查询和更新指令构成 了SQL的DML部分:

- SELECT - 从数据库表中获取数据
- UPDATE - 更新数据库表中的数据
- DELETE - 从数据库表中删除数据
- INSERT INTO - 向数据库表中插入数据
- SQL 的数据定义语言(DDL)部分使我们有能力创建或删除表格

​	我们也可以定义索引(键)，规定表之间的链接，以及施加表间的约 束。SQL 中最重要的 DDL 语句:

- CREATE DATABASE - 创建新数据库
- ALTER DATABASE - 修改数据库
- CREATE TABLE - 创建新表
- ALTER TABLE - 变更(改变)数据库表
- DROP TABLE - 删除表
- CREATE INDEX - 创建索引(搜索键)
- DROP INDEX - 删除索引

​	以下给出上述语句实例：

1. 创建数据库

    ```sql
   create DATABASE database-name
    ```

2. 删除数据库

   ```sql
   drop database dbname
   ```

3. 备份 SQL Server——创建备份数据的 device

   ```sql
   device use master EXECsp_addumpdevice 'disk', 'testBack', 'c:/msSQL7backup/MyNwind_1.dat'
   ```

4. 创建新表

   ```sql
   create table tabname(col1 type1 [not null] [primary key],col2 type2 [not null],..)
   ```

   根据已有的表创建新表:

   1. ```sql
      create table tab_new like tab_old
      ```

   2. ```sql
      create table tab_new as select col1, col2, ... from tab_old definition only
      ```

5. 删除新表

   ```sql
   drop table tabname
   ```

6. 增加列

   ```sql
   Alter table tabname add column col type
   ```

   > 列增加后，将不能删除。DB2 中列加上后数据类型也不能改变，
   >
   > 唯一能改变的是增加 varchar 类型的长度。

7. 主键的添加和删除

   ```sql
   -- 添加主键
   Alter table tabname add primary key(col)
   -- 删除主键
   Alter table tabname drop primary key(col)
   ```

8. 索引的创建和删除

   ```sql
   -- 索引的创建
   create [unique] index idxname on tabname(col....)
   -- 索引的删除
   drop index idxname
   ```

   > 索引是不可更改的，想更改必须删除重新建。

9. 视图的创建和删除

   ```sql
   -- 创建视图
   create view viewname as select statement
   -- 删除视图
   drop view viewname
   ```

10. 简单的基本的SQL语句

    ```sql
    -- 选择
    select * from table where field
    -- 插入
    insert into table1(field1,field2) values(value1,value2) -- 删除
    delete from table1 where field
    -- 更新
    update table1 set field1 = value1 where field
    -- 查找
    select * from table1 where field1 like '%value1%'
    -- 排序
    select * from table1 order by field1,field2 [desc] 
    -- 总数
    select count as totalcount from table1
    -- 求和
    select sum(field1) as sumvalue from table1
    -- 平均
    select avg(field1) as avgvalue from table1
    -- 最大
    select max(field1) as maxvalue from table1
    -- 最小
    select min(field1) as minvalue from table1
    ```

11. 高级查询运算词

    - UNION 运算符:UNION 运算符通过组合其他两个结果表(例如TABLE1 和 TABLE2)并消去表中任何重复行而派生出一个结果表。当 ALL 随 UNION 一起使用时(即 UNION ALL)，不消除重复行。两种情况 下，派生表的每一行不是来自 TABLE1 就是来自 TABLE2。

    - EXCEPT 运算符:EXCEPT 运算符通过包括所有在 TABLE1 中但不在 TABLE2 中的行并消除所有重复行而派生出一个结果表。当 ALL 随 EXCEPT 一起使用时 (EXCEPT ALL)，不消除重复行。

    - INTERSECT 运算符:INTERSECT 运算符通过只包括 TABLE1 和 TABLE2 中都有的行并消除所有重复行而派生出一个结果表。当 ALL 随 INTERSECT 一起使用时 (INTERSECT ALL)，不消除重复行。

    >  使用运算词的几个查询结果行必须是一致的。

## 3. Introduction of SQL Server 2008 Express Edition

### 3.1 数据库登陆

​	使用windows身份验证用本机名登陆连接到数据库服务器。

![2020-12-08-02.45.14.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-02.45.14.png)

​	此次实验选择的是默认实例：`.\SQLEXPRESS`。默认实例名与计算机名相同，但不称为“local”；一般情况下，如果要访问本机上的默认SQL服务器实例，使用计算机名、(local)、localhost、127.0.0.1、. 、本机IP地址，都可以达到相同的目的。但如果要访问非本机的SQL服务器，那就必须使用计算机/实例名的办法。命名实例的命名规则类似默认实例，只需要修改自定义的实例名称。实例名限制为16个字符且不区分大小写，实例名中的第一个字符必须是字母。

### 3.2 菜单栏

​	菜单栏是各种功能块的集合，包含文件、编辑、视图、工具、窗口、社区及帮助等板块，可以用来调节设置整个SQL Server 操作界面。

- **文件板块：**涉及的主要功能是SQL Server与对象资源管理器、数据库服务器以及数据库引擎的连接与断开等，常用菜单栏的文件板块快捷功能创建连接与数据库查询。
- **编辑板块：**提供撤销、重复等操作，包括基本的赋值、粘贴、剪切等，还可以进行文件或命令的查找与替换。
- **视图板块：**调整设置诸如对象资源管理器、属性窗口等其它各窗口的视图与布局等，同时工具栏还可以用来添加固定或取消设置快捷菜单功能，具体功能将在其它工具与功能中图解展示。

### 3.3 对象资源管理器

​	在对象资源管理器中可对现有资源进行管理、备份、还原等操作。对象资源管理器提供一个层次结构用户界面，用于查看和管理每个 SQL Server 实例中的对象。“对象资源管理器详细信息”窗格显示一个实例对象的表格视图以及用于搜索特定对象的功能。对象资源管理器的功能根据服务器的类型稍有不同，但一般都包括用于数据库的开发功能和用于所有服务器类型的管理功能。

### 3.4 SQL编辑器

​	在 sql 编辑器中可编写 sql 语句，查看 sql 执行结果及显示消息等。新建查询后会出现空白的 sql 编辑器，sql 语句的编写在编辑器内完成，编辑器上方显示该编辑器对应的连接参数。SQL Server 提供菜单图形界面进行 sql 查询的执行、调试等功能，用户编写 sql 语句后直接通过菜单功能键交互编译。sql 语句调试执行后，sql 编辑器下方会出现结果与调试窗口，供用户可视化地查看信息。

### 3.5 属性栏

​	属性栏可显示当前连接的各种参数，属性栏的位置和显示形式可在视图板块进行设置。

### 3.6 其他工具及视图

​	SQL Server 菜单栏的视图板块提供工具栏的设置，供用户选择添加移除快捷交互功能，包括：SQL 编辑器、XML 编辑器、文本编辑器、调试等，使用工具栏不仅帮助高效调试执行 sql 查询，还可以通过与菜单交互简化数据库查询的步骤和 sql 语句编写复杂度。

## 4. Create a Database

### 4.1 任务简介

​	进行sql语句练习之前需要创建数据库和数据表，并为数据表导入数据；下面将具体结合创建数据库及数据表的实例介绍相关的sql语法和命令形式，针对cap数据库的表customers、agents、products、orders逐步分析sql语句，同时就关系型数据库模型键的属性定理和空值的设置关注值得注意的细节，最后以图解的形式展示步骤流程；创建空表成功后将使用SQL Server的数据导入功能导入数据表的具体数据项，包括提前创建.txt文本文档以及导入数据过程的各项选择等，既介绍导入数据的步骤流程，又能熟悉SQL Server功能操作。

### 4.2 创建数据表

​	为了完成CAP数据库的创建，我们将在数据库中创建4个数据表。这4个数据表整合为CAP数据库。使用以下命令分别创建数据表：

```sql
-- create orders table
create table [dbo].[orders](
[ordno][char](4) NOT NULL,
[month][char](3) NULL,
[cid][char](4) NULL,
[aid][char](3) NULL,
[pid][char](3) NULL,
[qty][float] NULL,
[dollars][float] NULL,
PRIMARY KEY ([ordno]))

-- create agents table
create table [dbo].[agents](
[aid][char](3) NOT NULL,
[aname][char](10) NULL,
[city][char](13) NULL,
[percent][real] NULL,
PRIMARY KEY ([aid]))

-- create products table
create table [dbo].[products](
[pid][char](3) NOT NULL,
[pname][char](10) NULL,
[city][char](13) NULL,
[quantity][float] NULL,
[price][real] NULL,
PRIMARY KEY ([pid]))

-- create customers table
create table [dbo].[customers](
[cid][char](4) NOT NULL,
[cname][char](10) NULL,
[city][char](13) NULL,
[discnt][real] NULL,
PRIMARY KEY ([cid]))
```

### 4.3 导入数据

​	先为数据表创建文本文档记录所有数据项，注意数据项与属性一一对应并使用逗号，分隔；选中CAP数据库在“任务”中使用“导入数据”的功能，按照提示步骤依次选择数据来源、目标等，并确认映射和导入数据更新数据表。需要注意数据源和目标的正确选择，特别是文件类型和分隔符等；主要步骤遵循“SQL Server导入和导出”向导页面指引最终等待映射和检查，成功执行数据导入即可。同样可以使用`select *` 命令查看表。

```tex
% agents.txt
aid,aname,city,percent
a01,Smith,New York,6
a02,Jones,Newark,6
a03,Brown,Tokyo,7
a04,Gray,New York,6
a05,Otasi,Duluth,5
a06,Smith,Dallas,5

% orders.txt
ordno,month,cid,aid,pid,qty,dollars
1011,jan,c001,a01,p01,1000,450.00
1012,jan,c001,a01,p01,1000,450.00
1019,feb,c001,a02,p02,400,180.00
1017,feb,c001,a06,p03,600,540.00
1018,feb,c001,a03,p04,600,540.00
1023,mar,c001,a04,p05,500,450.00
1022,mar,c001,a05,p06,400,720.00
1025,apr,c001,a05,p07,800,720.00
1013,jan,c002,a03,p03,1000,880.00
1026,may,c002,a05,p03,800,704.00
1015,jan,c003,a03,p05,1200,1104.00
1014,jan,c003,a03,p05,1200,1104.00
1021,feb,c004,a06,p01,1000,460.00
1016,jan,c006,a01,p01,1000,500.00
1020,feb,c006,a03,p07,600,600.00
1024,mar,c006,a06,p01,800,400.00

% produxts.txt
pid,pname,city,quantity,price
p01,comb,Dallas,111400,0.50
p02,brush,Newark,203000,0.50
p03,razor,Duluth,150600,1.00
p04,pen,Duluth,125300,1.00
p05,pencil,Dallas,221400,1.00
p06,folder,Dallas,123100,2.00
p07,case,Newark,100500,1.00

% customers.yxy
cid,cname,city,discnt
c001,Tiptop,Duluth,10.00
c002,Basics,Dallas,12.00
c003,Allied,Dallas,8.00
c004,ACME,Duluth,8.00
c006,ACME,Kyoto,0.00
```

​	按照由平面文件源向SQL Server Native Client目标传输数据表，使用以下语句查看数据表中的内容：

```sql
-- look up for products
select * from products
-- look up for customers
select * from customers
-- look up for agents
select * from agents
-- look up for orders
select * from orders
```

## 5. Simple SQL Statements

1. find the aid values and names of agents that are based in New York.

   1. 语法知识点

      简单的select语句，select 属性为 aid 和 aname ，from 对象为agents，where条件限定 city=‘New York’。

   2. 分析

      题目要求查找agents表中城市为New York的aid和aname，同时select aid和aname使用“，”连接，在agents表中限制选择条件为where city=‘New York’。

      ```sql
      select aid, aname from agents 
      where city = 'New York'
      ```

   3. 查询结果

      ![2020-12-08-15.48.28.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-15.48.28.png)

      > 此题中不要求使用完全限定的表名，由于简单select语句只涉及到一个表，所以可以直接使用列名，city和agents.city在此题中等价。

2. Retrieve all pid values of parts for which orders are placed.

   1. 语法知识点

      简单select语句，在orders表中查询所有pid，select缺省distinct显示包括重复行的所有结果，磁体使用distinct查询所有非重复的pid。

   2. 分析

      检索所有订单中的pid值，出现在orders表中的pid即为拥有订单的pid，from对象为orders；查询所有pid值使用distinct去除重复；没有其它限制条件故where缺省。

      ```sql
      select distinct pid from orders
      ```

   3. 查询结果

      ![2020-12-08-16.00.50.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-16.00.50.png)

3. Retrieve all customer-agent name pairs, (cname, aname), where the customer places an order through the agent.

   1. 语法知识点

      简单select语句，查询不同表的属性组成的（caname，aname）对，需要连接customers、agents和orders三个表。使用from先求三个表的笛卡尔积；再使用aid连接agents和orders、cid连接customers和orders，where筛选customers.cid=orders.cid ，orders.aid=agents.aid，条件用and控制最终实现对三个表的连接；对连接的的新表投影求（caname，aname），找到有订单关联的值对（caname，aname）。

   2. 分析

      检索所有客户代理名称对（cname，aname）且客户通过该代理下订单。cname和aname属性属于不同的表，且要求有订单对应关系，需要连接orders、agents、customers组成新的表作为查询范围，使用aid和cid属性作为关联条件并用and控制符连接。

      From三个表的笛卡尔积，通过where对aid和cid属性进行筛选。连接得到aid、cid匹配的新表既反映订单关系，又同时包含cname和aname属性。最终直接在新表中投影select求（caname，aname）值对。

      ```sql
      select distinct customers.cname, agents.aname from customers, agents, orders
      where customers.cid = orders.cid and agents.aid = orders.aid
      ```

   3. 查询结果

      ![2020-12-08-16.12.40.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-16.12.40.png)

4. All pairs of customers based in the same city.

   1. 语法知识点

      使用别名和完全限定的表明属性，查询城市相同的aid：创建两个customers表实例并用别名区分，求两个customers表c1和c2的笛卡尔积作为from的查询范围，where筛选城市相同，最终使用有完全限定表名的属性select投影得到两个表的cid即一对满足条件的顾客对。

   2. 分析

      查询在同一城市的所有顾客对，命名两个customers表c1和c2求笛卡尔积，使用where选择城市相同且属于不同记录的两个顾客，select投影一组分别位于两个限定表的cid对，即城市相同的顾客对。

      ```sql
      select c1.cid, c2.cid from customers c1, customers c2
      where c1.city = c2.city and c1.cid < c2.cid
      ```

   3. 查询结果

      ![2020-12-08-16.21.57.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-16.21.57.png)

      > 涉及两个表需要创建别名并使用完全限定以区分属性，select语句中别名具有临时性，不用单独使用命名语句：表名+实例名即可，同时别名只在当前sql语句中有效。

5. Find pid values of products that have been ordered by at least two customers.

   1. 语法知识点

      使用表的别名编写查询语句，创建具有独立别名的实例，完全限定投影到由实例x1完全限定的cid属性。连接orders x1，x2两个实例，利用from求x1和x2笛卡尔积并借助where选择商品pid相同的不同cid顾客，最终投影x1范围变量的cid。

   2. 分析

      找到至少被两个顾客订购的产品pid值，即含有同一商品pid的订单记录至少对应两个不同的顾客cid，需要创建两个订单表orders实例并赋予别名，select对象是实例x1限定的pid属性。From求两个表的笛卡尔积以比对两个orders表中顾客cid的订单记录；where条件x1.pid=x2.pid保证订购同一产品，x1.cid<x2.cid保证是两个不同顾客的记录；最终由于笛卡尔积带来的记录组合重复问题，需要使用关键词distinct去除重复行并投影到pid得到结果。

      ```sql
      select distinct o1.pid 
      from orders o1, orders o2
      where o1.pid = o2.pid and o1.cid < o2.cid
      ```

   3. 查询结果

      ![2020-12-08-16.33.21.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-16.33.21.png)

      > 题目要求至少被两个顾客订购的产品，解题思路为求出所有拥有两个及以上顾客的商品pid，将至少条件转换为求最下限条件下的所有结果，只需要创建两个别名表即可。

6. Get cid values of customers who order a product for which an order is also placed by agent a06.

   1. 语法知识点

      此题需要先求被代理商a06订购的产品，再映射到订购了产品集合中任何产品的顾客，所以应该创建orders表上两个不同的范围变量。From求两个orders范围变量笛卡尔积，where条件使用pid将cid和aid=a06联系起来。

   2. 分析

      查询订购某个被代理商a06订购过的产品的顾客的cid值，首先查询被代理商a06订购的产品集合，select pid from orders where aid=‘a06’；再查询订购该结果集的顾客cid，创建另一个orders范围变量，使用表的别名借助where条件限制两个表pid属性值相等。整个sql语句是一个嵌套结构，from得到orders x和y的笛卡尔积；再where确定满足aid为a06的pid，并用“and”将pid相同的两个表的cid与条件aid=‘a06’关联 ，最终distinct关键字去重。

      ```sql
      select distinct cid from orders
      where pid in 
      (select pid from orders where aid = 'a06')
      ```

   3. 查询结果

      ![2020-12-08-16.57.08.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-16.57.08.png)

      > 涉及多个范围变量的sql查询一定要注意别名的使用，同时结果需要使用distinct去重。

7. Get cid values of customers who place orders with agents in Duluth or Dallas.

   1. 语法知识点

      IN谓词用在子查询语句中，用来实现在一个select语句中嵌套另一个select语句，一般出现在where中连接两个select语句，作为外层select语句where条件的限制。子查询作为值集返回以解决外层select查询，IN就是子查询与外层查询连接的重要谓词。例如此题中城市在Duluth和Dallas的aid结果集通过in成为aid的限制条件，服务于外层select语句对cid的查询。

   2. 分析

      求通过住在Duluth或Dallas的代理商订了货的顾客的cid值，首先查询住在Duluth或Dallas的代理商，其次将结果集aid作为外层select语句的值集，用在where条件中限制aid帮助在orders表中选择记录，即外层select语句的结果被限定为orders表中aid为改值集的成员的行，最终去重distinct后投影到cid求得顾客cid结果集。

      ```sql
      select distinct cid from orders
      where aid in
      (select aid from agents where city = 'Duluth' or city = 'Dallas')
      ```

   3. 查询结果

      ![2020-12-08-17.08.31.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-17.08.31.png)

8. To retrieve all information concerning agents based in Duluth or Dallas .(very close to the Subquery in the previous example).

   1. 语法知识点

      IN谓词除了用于子查询，还可以作为简单select语句中where条件的属性限定，相当于“=”，一般用于值对条件的选择。Expr in(subquery)或expr in(val),即in连接子查询或者赋值常数（序列）给表达式。

   2. 分析

      查询所有住在Duluth或Dallas的代理商的所有信息。使用简单select语句在agents中选择city为Duluth或Dalla的代理商所有信息。有两种方法：使用谓词IN或用“or”连接一般选择条件“=”赋值语句。

      ```sql
      -- (i)
      select * from agents
      where city in ('Duluth', 'Dallas')
      -- (ii)
      select * from agents
      where city = 'Duluth' or city = 'Dallas'
      ```

   3. 查询结果

      ![2020-12-08-18.18.53.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-18.18.53.png)

9. To determine the names and discounts of all customers who place orders through agents in Duluth or Dallas.

   1. 语法知识点

      IN谓词支持的子查询的多层嵌套，代理商aid集作为顾客cid集的子查询结果，顾客cid集作为最外层select语句cname、discnt的子查询。

   2. 分析

      求出通过住在Duluth或Dallas的代理商订货的所有顾客的姓名和 折扣。首先查询住在Duluth或Dallas的代理商作为最内层子查询，其次查询通过改代理商aid集订货的顾客cid集，最后select cid作为子查询返回结果，供最外层查询在customers表中select canme和discnt。

      ```sql
      select distinct cname, discnt from customers
      where cid in
      (select cid from orders where aid in
      (select aid from agents where city = 'Duluth' or city = 'Dallas'))
      ```

   3. 查询结果

      ![2020-12-08-18.34.39.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-18.34.39.png)

10. To find the names of customers who order product p05.

    1. 语法知识点

       子查询除了类似题九等内层子查询完全独立于外层子查询的非相关子查询，还有此题代表的向内层子查询提供来自外层select语句数据的更一般情况。外层selec语句where条件直接向内层子查询提供具体的属性值作为内层子查询的结果，外层select语句提供的变量限定内层子查询，而子查询的实现又反过来作为外层select语句的选择条件。

    2. 分析

       查询订购了产品p05的顾客的名字，使用相关子查询即外部select向内部子查询传递变量相互关联。外部select语句限定子查询的pid结果为p05，即子查询需要查询商品p05的顾客cid；子查询的cid与外部select语句的customers.cid关联，即子查询确定了外部select语句的cid值集；最终由外部select在customers中查询cid为子查询限定的cname结果。

       ```sql
       -- (i)
       select distinct cname from customers
       where cid in 
       (select cid from orders where pid = 'p05')
       -- (ii)
       select distinct cname from customers, orders
       where customers.cid = orders.cid and orders.pid = 'p05'
       ```

    3. 查询结果

       ![2020-12-08-18.44.10.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-18.44.10.png)

11. Get the names of customers who order product p07 from  agent a03.

    1. 分析

       查询从代理商a03处订购了产品p07的顾客的名字，子查询为查询在orders表搜索pid为p07且aid为a03的顾客cid，再将子查询的cid作为外层select语句where条件的cid值集，在customers表中选择cid属于值集的记录，最终投影到cname得到结果。

       ```sql
       select distinct cname from customers
       where cid in
       (select cid from orders where pid = 'p07' and aid = 'a03')
       ```

    2. 查询结果

       ![2020-12-08-18.49.54.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-18.49.54.png)

12. To retrieve ordno values for all orders placed by customers in Duluth through agents in New York.

    1. 语法知识点

       Expr IN（subquery）通过求解子查询返回一个值，再由外层select语句进行成员资格测试。

       Exists谓词测试被子查询检索到的行集是否为非空，exists（subsquery）为真当且仅当子查询返回一个非空的集合。

       IN和exists类似，作为连接子查询和外层select的谓词，用来表示子查询结果是否返回给外层查询作为条件值集。

    2. 分析

       查询住在Duluth的顾客和住在New York的代理商组成的所有订货记  录的ordno值。使用谓词IN：分别创建两个子查询检索住在Duluth的aid和住在New York的cid，使用and连接将结果集求并返回给外层select语句，外层select语句zaiorders表中根据子查询对记录筛选，确定住在Duluth的顾客和住在New York的代理商组成的所有订货记录的ordno。使用谓词exists同样先用子查询确定住在Duluth的顾客和住在New York的代理商组成的所有订货记录，再将结果集返回给外层select作为资格测试条件；子查询内部可以使用简单select语句对customers和agents求笛卡尔积再筛选。

       ```sql
       select distinct cname, discnt from customers
       where cid in
       (select cid from orders where aid in
       (select aid from agents where city = 'Duluth' or city = 'Dallas'))
       ```

    3. 查询结果

       ![2020-12-08-21.17.26.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-21.17.26.png)

13. Find aid values of agents with a minimum percent commission.

    1. 语法知识点

       使用函数min求最小值，用在子查询中将结果集返回给外层select语句作为where中的选择条件。

    2. 分析

       查询折扣最小的代理，子查询使用min函数查询最小的折扣值，将结果作为percent的选择条件作用于外层select语句的where，最后投影到aid确定代理商。

       ```sql
       -- (a)
       select aid from agents
       where [percent] <= all (select [percent] from agents)
       -- (b)
       select aid from agents
       where [percent] = (select min([percent]) from agents)
       ```

    3. 查询结果

       ![2020-12-08-21.30.51.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-21.30.51.png)

14. Find all customers who have the same discount as that of any of the customers in Dallas or Boston.

    1. 语法知识点

       量化比较谓词用在一个简单的表达式值和子查询的结果进行比较时的结果判断，其中some与IN具有完全相同的效果。

    2. 分析

       找出与住在Dallas或Boston的顾客拥有相同折扣的所有顾客，使用子查询的方式，首先查询住在Dallas或Boston的顾客拥有的折扣，再使用谓词some保证外层select结果记录的discnt值与子查询结果集中至少一个元素相等。

       ```sql
       select cid, cname from customers
       where discnt = some(
       select discnt from customers where city = 'Dallas' or city = 'Boston'
       )
       ```

    3. 查询结果

       ![2020-12-08-21.40.55.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-21.40.55.png)

15. Get cid values of customers with discnt smaller than those of any customers who live in Duluth.

    1. 语法知识点

       量化比较谓词 <all 要求被选择行的某一特定属性值小于由子查询返回的所有值。

    2. 分析

       找出与住在Dallas或Boston的顾客拥有相同折扣的所有顾客，使用子查询的方式，首先查询住在Dallas或Boston的顾客拥有的折扣，再使用谓词some保证外层select结果记录的discnt值与子查询结果集中至少一个元素相等。

       ```sql
       select cid from customers
       where discnt < ALL(select discnt from customers where city = 'Duluth')
       ```

    3. 查询结果

       ![2020-12-08-22.10.58.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.10.58.png)

16. Retrieve all customer names where the customer places an order through agent a05.

    1. 语法知识点

       Exists谓词和in谓词都是将结果集返回给外层子查询为true。

    2. 分析

       查询所有通过代理a05订购商品的顾客名，有三种方法：使用in谓词在子查询中检索cid为a05的记录的cid并返回结果；使用exists子查询的选择序列为*，向外层语句返回代理为a05且cid相同为条件得到的同一记录集；不使用嵌套查询，用from求笛卡尔积再选择投影。

       ```sql
       -- (a)
       select cname from customers
       where cid in(
       select cid from orders where aid = 'a05'
       )
       -- (b)
       select distinct cname from customers
       where exists (
       select * from orders where customers.cid = orders.cid and orders.aid = 'a05'
       ) 
       -- (c)
       select distinct cname from customers, orders
       where customers.cid = orders.cid and orders.aid = 'a05'
       ```

    3. 查询结果

       ![2020-12-08-22.18.07.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.18.07.png)

17. Get cid values of customers who order both products p01 and p07.

    1. 分析

       查询同时订购了商品p01和p07的顾客，可以使用exists嵌套查询，也可以简单select语句笛卡尔积选择投影。

       ```sql
       -- (a)
       select distinct cid from orders
       where pid = 'p01' and cid in
       (select cid from orders where pid = 'p07')
       -- (b)
       select distinct o1.cid from orders o1, orders o2
       where o1.cid = o2.cid and o1.pid = 'p01' and o2.pid = 'p07'
       -- (c)
       select distinct cid from orders o1
       where pid = 'p01' and exists
       (select * from orders o2 where o1.cid = o2.cid and pid = 'p07')
       ```

    2. 查询结果

       ![2020-12-08-22.28.46.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.28.46.png)

18. Retrieve all customer names where the customer does not place an order through agent a05.

    1. 语法知识点

       Not exists与exists应用的逻辑条件想法，not exists为true时子查询不向外层select语句返回查询结果集。

    2. 分析

       查询没有通过代理商a05订货的所有顾客的名字。使用not exists 子查询检索通过代理a05订货的顾客cid，再将非子查询结果集返回给外层select语句，相当于求差集排除通过代理a05订货的顾客cid，得到没有通过代理商a05订货的所有顾客的名字。

       ```sql
       select distinct cname from customers
       where not exists
       (select * from orders where customers.cid = orders.cid and orders.aid = 'a05')
       ```

    3. 查询结果

       ![2020-12-08-22.32.38.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.32.38.png)

19. Retrieving all customer names where the customer does not place an order through agent a05, but using the two equivalent NOT IN and <> ALL predicates in place of NOT EXISTS.

    1. 检索没有通过 a05 下订单的客户，要使用 NOT IN 以及<>替代 NOT EXISTS。(与上一题类似)

       ```sql
       select distinct cname
       from customers
       where cid not in
       (select cid from orders where aid='a05')
       
       select distinct cname
       from customers
       where cid <> all
       (select cid from orders where aid='a05')
       ```

    2. 查询结果

       ![2020-12-08-22.38.33.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.38.33.png)

20. Find cid values of customers who do not place any order through agent a03.

    1. 分析

       查询没有通过代理商a03订货的顾客cid与上一题思路相同，使用not exists谓词再子查询中注意检索*全部记录。

       ```sql
       select cid
       from customers
       where cid not in
       (select cid from orders where aid='a03')
       ```

    2. 查询结果

       ![2020-12-08-22.44.35.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.44.35.png)

21. Retrieve the city names containing customers who order product p01. 

    1. 分析

       查询所有订购过商品p01的顾客，可以通过子查询使用谓词in、exists、some，相关性查询传递变量以及简单select语句五种方法实现。

       ```sql
       select distinct city from customers
       where cid in
       (select cid from orders where pid = 'p01')
       ```

    2. 查询结果

       ![2020-12-08-22.59.57.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-22.59.57.png)

22. To create a list of cities where either a customer or an agent, or both, is based.

    1. 语法知识点

       Union谓词对应关系代数中的并运算，可以将多个属性或记录并联。

    2. 分析

       创建客户或代理（或两者）所在城市的列表，选出的同一个属性city在不同表中的记录，通过谓词并union合并起来。

       ```sql
       select city from customers union select city from agents
       ```

    3. 查询结果

       ![2020-12-08-23.05.26.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.05.26.png)

23. Get the cid values of customers who place orders with  all agents based in New York.

    1. 语法知识点

       对应关系 嵌套结构 特殊谓词 语法 套路模板/方法

    2. 分析

       获取通过在纽约的所有代理商下订单的客户的cid值。多层嵌套语句两次使用not exists构成双重否定，即将题目的逻辑关系转换为检索所有cid值，这些cid集合中的每一个cid元素对应的记录包含所有在纽约的代理商。双重否定表示肯定，通过not exists实现对“所有”这一条件的查询。

       ```sql
       select c.cid from customers c  
       where not exists  
       (select * from agents a 
       where a.city = 'New York' and not exists  
       (select * from orders x 
       where x.cid = c.cid and x.aid = a.aid))
       ```

    3. 查询结果

       ![2020-12-08-23.09.29.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.09.29.png)

24. Get the aid values of agents in New York or Duluth who place orders for all products costing more than a dollar.

    1. 分析

       查询所有住在New York或Duluth的代理商，这些代理商的多有订单都超过1美元。同样使用not exists谓词，外层select语句的where条件既选择住在New York或Duluth的代理商，又通过and同时满足not exists连接的订单价格超过1美元的子查询条件。

       ```sql
       select aid from agents a 
          where (a.city = 'New York' or a.city = 'Duluth') 
          and not exists  
       (select p.pid from products p 
       where p.price > 1.00 and not exists  
       (select * from orders x 
       where x.pid = p.pid and x.aid = a.aid))
       ```

    2. 查询结果

       ![2020-12-08-23.13.00.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.13.00.png)

25. Find aid values of agents who place orders for product p01 as well as for all products costing more than a dollar.

    1. 分析

       查找订购产品p01以及所有成本超过1美元的产品的代理商。同样使用not exists谓词和双重否定的解题逻辑。

       ```sql
       select o1.aid from orders o1
       where o1.pid = 'p01' and not exists
       (select p.pid from products p where p.price > 1.00 and not exists
       (select * from orders o2 where p.pid = o2.pid and o1.aid = o2.aid))
       ```

    2. 查询结果

       ![2020-12-08-23.26.54.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.26.54.png)

26. Find pid values of products supplied to all customers in Duluth.

    1. 分析

       查找被所有住在Duluth的顾客订购的产品pid，题目要求被查找所 有顾客订购的产品，使用not exists两次嵌套子查询；where条件选择使用and连接city=‘Duluth’条件限定顾客集。

       ```sql
       select pid from products
       where not exists
       (select cid from customers where customers.city = 'Duluth' and not exists
       (select * from orders where orders.cid = customers.cid and products.pid = orders.pid))
       ```

    2. 查询结果

       ![2020-12-08-23.33.18.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.33.18.png)

27. Determine the total dollar amount of all orders.

    1. 语法知识点

       简单select语句使用函数sum统计求和，语法：

       Sum（属性）as结果集名称。

    2. 分析

       确定所有订单的总金额，使用sum函数求orders表中dollars列的数值和，并将结果集命名为totaldollars，简单select语句直接处理dollars属性，不用附加where进行条件选择。

       ```sql
       select sum(dollars) as totaldollars from orders
       ```

    3. 查询结果

       总额为9802.

28. To determine the total quantity of product p03 that has been ordered.

    1. 分析

       确定被订购的chanpinp03的总数量。同样使用sum函数处理qty属性，使用select语句where添加一个选择条件pid=‘p03’。

       ```sql
       select sum(qty) as TOTAL from orders where pid = 'p03'
       ```

    2. 查询结果

       总额为2400.

29. Get the number of cities where customers are based.

    1. 语法知识点

       Count函数计算属性数量即指定列行数。

    2. 分析

       确定顾客所在城市的数量，子啊customers表中计数city列的行数。

       ```sql
       select COUNT(distinct city) from customers
       ```

    3. 查询结果

       城市数量为3.

30. List the cid values of alt customers who have a discount less than the maximum discount.

    1. 语法知识点

       Max函数用来求属性最大数值，比较关系符<处理属性之间的大小关 系作为限定条件选择记录。

    2. 分析

       列出折扣低于最大折扣的顾客，先用max函数求customers表中的最大折扣，再用<限制满足地域最大折扣的discnt，并以此为条件资格选择记录，最终投影到cid得到顾客cid集。

       ```sql
       select cid from customers where discnt < (select max(discnt) from customers)
       ```

    3. 查询结果

       ![2020-12-08-23.54.10.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.54.10.png)

31. Find products ordered by at least two customers.

    1. 分析

       查询至少被两个顾客订购的商品，使用比较运算符<=，通过嵌套子查询得到此题的新解法

       ```sql
       select p.pid from products p 
       where 2 <= (select count(distinct cid) from orders where pid=p.pid)
       ```

    2. 查询结果

       ![2020-12-08-23.56.46.png](http://panzy25.ticp.io:4000/images/2020/12/08/2020-12-08-23.56.46.png)

32. Add a row with specified values for columns cid, cname, and city (c007, Windix, Dallas, null)to the customers table.

    1. 语法知识点

       Insert语句为基本sql语句为数据表增添新纪录。

    2. 分析

       将列cid、cname和city（c007、Windix、Dallas、null）的指定值的行添加到customers表中。

       ```sql
       insert into customers(cid, cname, city) 
       values ('c007', 'Windix', 'Dallas')
       ```

    3. 查询结果

       ![2020-12-09-00.15.28.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-00.15.28.png)

33. After inserting the row (c007, Windix, Dallas, null) to the customers table in Example 3.7.7, assume that we wish to find the average discount of all customers.

    1. 分析

       在将行（c007，Windix，Dallas，null）插入示例3.7.7中的customers表之后，找到所有客户的平均折扣，直接使用函数avg对属性discnt求平均值。

       ```sql
       select AVG(discnt) from customers
       ```

    2. 查询结果

       ​	平均值为7.6.

34. To calculate the total product quantity ordered of each individual product by each individual agent.

    1. 语法知识点

       Group by进行分组操作，经常配合函数使用作为统计资格筛选。

    2. 分析

       计算每个代理商订购的每个单独产品的总产品数量，通过pid、cid属性进行分组，再对qty进行sum函数求和。

       ```sql
       select pid, aid, sum(qty) as total from orders 
       group by pid, aid
       ```

    3. 查询结果

       ![2020-12-09-00.54.38.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-00.54.38.png)

35. Print out the agent name and agent identification number, and the product name and product identification number, together with the total quantity each agent supplies of that product to customers c002 and c003.

    1. 分析

       打印代理商名称和代理商识别号、产品名称和产品识别号，以及每个代理商向客户c002和c003供应该产品的总数量。

       ```sql
       select aname, a.aid, pname, p.pid, sum(qty) as total
        from orders x, products p, agents a 
        where x.pid = p.pid and x.aid = a.aid and x.cid in ('c002', 'c003') 
        group by a.aid, a.aname, p.pid, p.pname 
       ```

    2. 查询结果

       ![2020-12-09-01.01.58.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.01.58.png)

36. Print out all product and agent IDs and the total quantity ordered of the product by the agent, when this quantity exceeds 1000.

    1. 语法知识点

       Having条件查询相当于where，为select语句限制选择条件，一般与函数搭配使用。

    2. 分析

       当数量超过1000时，打印出所有产品和代理商的ID以及代理商订购的产品总量。使用sum函数，并用having条件选择总量大于1000的记录。

       ```sql
       select pid, aid, sum(qty) as total from orders 
       group by pid, aid having sum(qty) > 1000
       ```

    3. 查询结果

       ![2020-12-09-01.05.50.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.05.50.png)

37. Provide pid values of all products purchased by at least two customers.

    1. 分析

       提供至少被两个顾客订购的所有商品的pid，将题目转换为在orders表中根据pid进行分组，即分组获取每个pid的所有记录，再用函数count分别统计每个pid记录对应cid数量，只要pid对应的cid数大于等于2即为至少被两个顾客订购。

       ```sql
       select distinct pid from orders 
       group by pid 
       having count(distinct cid) >= 2 
       ```

    2. 查询结果

       ​	![2020-12-09-01.08.11.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.08.11.png)

38. List all customers, agents, and the dollar sales for  pairs of customers and agents, and order the result from largest to smallest sales totals. Retain only those pairs for which the dollar amount is at least equal to 900.00.

    1. 语法知识点

       Order by对结果集进行排序，此题中order by casales desc即以销售额从大到小排序，casales为销售额的属性名称。

    2. 分析

       列出所有客户、代理商以及成对客户和代理商的美元销售额，并按销售额从大到小的顺序排列结果。仅保留美元金额至少等于900.00的对。

       ```sql
       select c.cname, c.cid, a.aname, a.aid, sum(dollars) as casales 
       from customers c, orders o, agents a 
       where c.cid = o.cid and a.aid = o.aid 
       group by c.cname, c.cid, a.aname, a.aid 
       having sum(o.dollars) >= 900.00 
       order by casales desc
       ```

    3. 查询结果

       ![2020-12-09-01.10.28.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.10.28.png)

39. Listed the cid values of all customers with a discount less than the maximum discount.

    1. 分析

       列出所有客户的CID值，折扣低于最大折扣，接替思路与前面的例题类似：再子查询中使用max函数并用比较运算符选择条件属性。

       ```sql
       select cid from customers 
       where discnt < (select max(discnt) from customers)
       ```

    2. 查询结果

       ![2020-12-09-01.13.36.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.13.36.png)

40. Retrieve the maximum discount of all customers.

    1. 分析

       求顾客的最大折扣，直接使用max函数即可。

       ```sql
       select max(discnt) from customers
       ```

    2. 查询结果

       最大结果为12。

41. Retrieve all data about customers whose cname begins with the letter “A”.

    1. 分析

       检索以A开头的顾客的所有信息，以A开头表示为like‘A%’，使用like。检索所有信息用*。

       ```sql
       select * from customers where cname like 'A%'
       ```

    2. 查询结果

       ![2020-12-09-01.19.44.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.19.44.png)

42. Retrieve cid values of customers whose cname does not have a third letter equal to “%”.

    1. 语法知识点

       LIKE操作符的通配符：

       百分号（%）：表示任何字符出现任何次数（'%'不会匹配到值NULL）

       下划线（_）：匹配单个的任意字符

    2. 分析

       检索cname没有第三个字母等于“%”的客户的cid值。

       ```sql
       select cid from customers where cname not like '__[%]%'
       select cid from customers where cname not like 
       '__\%%' escape '\'
       ```

    3. 查询结果

       ![2020-12-09-01.32.58.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.32.58.png)

43. Retrieve cid values of customers whose cname begins “Tip_” and has an arbitrary number of characters following.

    1. 分析

       检索其cname以“Tip_u”开头且后面有任意数量字符的客户的cid值。

       ```sql
       select cid from customers where cname like 'TIP[_]%'
       select cid from customers where cname like 'TIP\_%' escape '\'
       ```

    2. 查询结果

       ![2020-12-09-01.35.48.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.35.48.png)

44. Retrieve cid values of customers whose cname starts with the sequence “ab\”.

    1. 分析

       检索cname以“ab”序列开头的客户的cid值。

       ```sql
       select cid from customers where cname like 'ab\%'
       ```

    2. 查询结果

       ![2020-12-09-01.39.01.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.39.01.png)

45. Add a row with specified values to the orders table, setting the qty and dollars columns null.

    1. 语法知识点

       Insert向已有数据表中插入新纪录。

    2. 分析

       将具有指定值的行添加到orders表，将“数量”和“美元”列设置为空。

       ```sql
       insert into orders (ordno, month, cid, aid, pid) values (1107, ‘aug’, ‘c006’, ‘a04’, ‘p01’) 
       ```

    3. 查询结果

       ![2020-12-09-01.42.18.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.42.18.png)

46. Create a new table called swcusts of Southwestern customers, and insert into it all customers from Dallas and Austin.

    1. 语法知识点

       Create创建新的数据表。

       insert向已有数据表中添加新纪录。

    2. 分析

       创建一个名为swcusts的新表southern customers，并将来自达拉斯和奥斯汀的所有客户插入其中。

       ```sql
       create table swcusts ( 
       cid char(4) not null,  
       cname varchar(13), 
       city varchar(20), 
       discnt real)
       insert into swcusts 
       select * from customers 
       where city in ('Dallas', 'Austin') 
       ```

    3. 查询结果

       ![2020-12-09-01.46.47.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.46.47.png)

47. Give all agents in New York a 10% raise in the percent commission they earn on an order.

    1. 分析

       给所有在纽约的代理商10%的提成。使用update更新数据即可。

       ```sql
       update agents set [percent] = 1.1 * [percent] where city = 'New York'
       ```

    2. 查询结果

       ![2020-12-09-01.51.23.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.51.23.png)

48. Give all customers who have total orders of more than $1000 a 10% increase in the discnt.

    1. 分析

       向所有订单总额超过1000美元的客户提供折扣，每个记录增加10%。

       ```sql
       update customers set discnt = 1.1 * discnt  
       where cid in 
        (select cid from orders group by cid having sum(dollars) > 1000)
       ```

    2. 查询结果

       ![2020-12-09-01.56.08.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-01.56.08.png)

49. Delete all agents in New York.

    1. 分析

       删除所有在New York的代理，直接使用delete语句。

       ```sql
       delete from agents where city = 'New York'
       ```

    2. 查询结果

       <img src="http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-02.00.40.png" alt="2020-12-09-02.00.40.png" style="zoom:130%;" />

50. Delete all agents who have total orders of less than $600.

    1. 分析

       删除所有订单总额少于600美元的代理。使用子查询，首先查询订单总额小于600美元的代理：通过having子句配合group对sum函数进行分组统计过滤；外层sql语句使用delete语句，删除所有子查询返回的aid结果集。

       ```sql
       Delete from agents where aid in 
       (select aid from orders 
       Group by aid 
       having sum(dollars)<600)
       ```

    2. 查询结果

       ![2020-12-09-02.04.18.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-02.04.18.png)

51. Retrieve the names of customers who order products costing $0.50.

    1. 分析

       查询所有订购商品价格位0.50美元的顾客名称。范围变量涉及三个表customers、orders和products，求三个表的笛卡尔积，通过cid和pid属性使用and控制符连接三个表，where条件选择price为0.50的记录，最终投影到cname得到顾客名称集。

       ```sql
       select cname from customers c, orders x, products p 
       where c.cid = x.cid and x.pid = p.pid and p.price = 0.50
       ```

    2. 查询结果

       ![2020-12-09-02.06.07.png](http://panzy25.ticp.io:4000/images/2020/12/09/2020-12-09-02.06.07.png)





































