# 数据库第一次作业:

<center>数据库系统安装作业</center>



> written by panzy25, 18372046
>
> on Typora
>
> Based on Markdown language 



**CONTENT：**

[toc]

## 1. 查询以及下载软件安装包

​	根据当前计算机的基本信息：例如计算机系统的操作系统版本，操作系统的位长，硬件基本信息等，结合MicroSoft提供的有关SQL Server软件及其组件的相关版本信息、版本类别以及更新级别，对需要下载的软件版本进行挑选。

### 1.1 查询本计算机的基本信息

![0.png](http://panzy25.ticp.io:4000/images/2020/09/08/0.png)

<center>图1</center>
根据在Windows系统的计算机基本信息查询界面，了解到当前主机装载的硬件信息。

* 处理器：AMD Ryzen 5 3600 6-Core Processor 3.60GHz
* 内存：32.0 GB
* 系统类型：64bit，基于x64的命令集



### 1.2 查询SQL Server的相关版本信息

​	前往[微软官方网站](https://support.microsoft.com/zh-cn/help/321185/how-to-determine-the-version-edition-and-update-level-of-sql-server-an)确定SQL Server及其组件的版本、版本类别和更新级别。下将会文介绍如何确定当前的 Microsoft SQL Server 版本号以及相应的服务或 Service Pack 级别。 还介绍了如何确定正在使用的 SQL Server 的特定版本。



#### 1.2.1 如何确定当前的 Microsoft SQL Server 版本号

​	以下提供5种方法来确定当前 Microsoft SQL Server 版本号：



1. 通过使用 SQL Server Management Studio 中的对象资源管理器连接到服务器。 连接对象资源管理器后，它将显示版本信息（在括号中），以及用于连接到 SQL Server 特定实例的用户名。

2. 查看该实例的错误日志文件的前几行。 默认情况下，错误日志位于 Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG 和 ERRORLOG.*n* 文件中。 条目可能类似于以下内容：

   ```
   2011-03-27 22:31:33.50 Server      Microsoft SQL Server 2008 (SP1) - 
   10.0.2531.0 (X64)
   
                   March 29 2009 10:11:52
   
                   Copyright (c) 1988-2008 Microsoft Corporation
   
   Express Edition (64-bit)
   on Windows NT 6.1 <X64> (Build 7600: ) 
   ```

   此条目提供了有关该产品的所有必要信息，例如版本、产品级别、64 位还是 32 位、SQL Server 的版本类别以及运行 SQL Server 的操作系统版本。

3. 连接到 SQL Server 的实例，然后运行以下查询：

   ```
   Select @@version 
   ```

   此查询的输出示例如下：

   ```
   Microsoft SQL Server 2008 (SP1) - 
   10.0.2531.0 (X64)
     March 29 2009 10:11:52 Copyright (c) 1988-2008 Microsoft Corporation
   Express Edition (64-bit)
     on Windows NT 6.1 <X64> (Build 7600: ) 
   ```

   在SQLServer中显示如下：

   

   ![0.5.jpg](http://panzy25.ticp.io:4000/images/2020/09/08/0.5.jpg)

<center>图2</center>

4. 连接到 SQL Server 的实例，然后在 SQL Server Management Studio (SSMS) 中运行以下查询：

```
	SELECT SERVERPROPERTY('productversion'), SERVERPROPERTY ('productlevel'),

	SERVERPROPERTY ('edition') 
```

​		**注意**：此查询适用于 SQL Server 2000 或更高版本的任何实例。

5. 从 SQL Server 2008 开始，您还可以使用“已安装的 SQL 服务器功能发现”报告。 此报告可以通过定位 SQL 服务器安装中心的**工具**页来找到。 此工具提供有关系统上安装的所有 SQL Server 实例的信息。 这些包括客户工具，如 SQL Server Management Studio。 唯一要注意的是，此工具只能在安装 SQL Server 的系统上本地运行。 它不能用于获取有关远程服务器的信息。

   示例报告的快照如下：

   

   ![0.6.png](http://panzy25.ticp.io:4000/images/2020/09/08/0.6.png)

   <center>图3</center>

#### 1.2.2 如何确定SQL Server相应的服务或 Service Pack 级别

​	通过[Microsoft SQL Server 支持生命周期页](https://support.microsoft.com/zh-cn/lifecycle?c2=1044)来查看有关 SQL Server 支持生命周期的信息。在表格中可以看到**适用于 SQL Server 的当前受支持版本的最新更新**。



| 已发布产品                                                   | 生命周期开始日期 | 主要支持结束日期 | 外延支持结束日期 | Service Pack 支持结束日期 | 注释                                                         |
| :----------------------------------------------------------- | :--------------- | :--------------- | :--------------- | :------------------------ | :----------------------------------------------------------- |
| Microsoft SQL 2005 Server Enterprise                         | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。有关 SQL Server 2005 支持的更多信息，请参阅此链接：[www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL 2005 Server Workgroup                          | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2000 64-bit Edition                     | 2000/11/30       | 不适用           | 不适用           | 2002/7/11                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Developer Edition                  | 2000/11/30       | 不适用           | 不适用           | 2002/7/11                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Enterprise Edition                 | 2000/11/30       | 不适用           | 不适用           | 2002/7/11                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Service Pack 1                     | 2001/6/12        | 不适用           | 不适用           | 2002/2/28                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Service Pack 2                     | 2001/11/30       | 不适用           | 不适用           | 2003/4/7                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Service Pack 3a                    | 2003/1/7         | 不适用           | 不适用           | 2007/7/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Service Pack 4                     | 2005/5/6         | 2008/4/8         | 2013/4/9         |                           | 此产品的支持已终止。可在[此处](https://docs.microsoft.com/zh-cn/sql/sql-server/end-of-support/sql-server-end-of-life-overview)找到迁移指导。 |
| Microsoft SQL Server 2000 Windows CE Edition 2.0             | 2002/12/16       | 2008/1/8         | 2013/1/8         |                           | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 Workgroup Edition                  | 2005/6/1         | 2008/4/8         | 2013/4/9         |                           | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2000 标准版                             | 2000/11/30       | 不适用           | 不适用           | 2002/7/11                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2005 Compact Edition                    | 2007/2/19        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Developer Edition                  | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Enterprise Edition for Itanium Based Systems | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Enterprise X64 Edition             | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Express Edition                    | 2006/6/1         | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Express Edition with Advanced Services | 2006/7/16        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Service Pack 1                     | 2006/4/18        | 不适用           | 不适用           | 2008/4/8                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2005 Service Pack 2                     | 2007/2/19        | 不适用           | 不适用           | 2010/1/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2005 Service Pack 3                     | 2008/12/15       | 不适用           | 不适用           | 2012/1/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2005 Service Pack 4                     | 2010/12/13       | 2011/4/12        | 2016/4/12        |                           | 此产品的支持已终止。可在[此处](https://docs.microsoft.com/zh-cn/sql/sql-server/end-of-support/sql-server-end-of-life-overview)找到迁移指导。 |
| Microsoft SQL Server 2005 Standard Edition                   | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Standard Edition for Itanium Based Systems | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2005 Standard X64 Edition               | 2006/1/14        | 不适用           | 不适用           | 2007/7/10                 | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。 有关 SQL Server 2005 产品的信息，请参阅此链接： [www.microsoft.com/sqlserverupgrade](https://support.microsoft.com/www.microsoft.com/sqlserverupgrade) |
| Microsoft SQL Server 2008 R2 Service Pack 1                  | 2011/7/12        | 不适用           | 不适用           | 2013/10/8                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2008 R2 Service Pack 2                  | 2012/7/26        | 不适用           | 不适用           | 2015/10/13                | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。 对 SP2 的支持将于 2019 年 7 月 9 日终止（仅适用于 IA64）。有关详细信息，请参阅[博客](http://blogs.msdn.com/b/sqlreleaseservices/archive/2014/09/26/sql-server-2008-r2-service-pack-3-has-released.aspx)“SQL 版本服务”。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| Microsoft SQL Server 2008 Service Pack 1                     | 2009/3/31        | 不适用           | 不适用           | 2011/10/11                | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2008 Service Pack 2                     | 2010/9/24        | 不适用           | 不适用           | 2012/10/9                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2012 Service Pack 1                     | 2012/11/7        | 不适用           | 不适用           | 2015/7/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2012 Service Pack 2                     | 2014/6/10        | 不适用           | 不适用           | 2017/1/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2012 Service Pack 3                     | 2015/12/1        | 不适用           | 不适用           | 2018/10/9                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 2014 Service Pack 1                     | 2015/4/14        | 不适用           | 不适用           | 2017/10/10                | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server 4.2 for OS/2                            | 不适用           | 1999/7/1         | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.0 标准版                              | 不适用           | 1999/3/31        | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 Enterprise Edition                  | 1998/3/1         | 2004/3/31        | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 Service Pack 1                      | 不适用           | 不适用           | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 Service Pack 2                      | 不适用           | 不适用           | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 Service Pack 3                      | 不适用           | 不适用           | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 Service Pack 4                      | 不适用           | 不适用           | 不适用           | 1999/3/24                 |                                                              |
| Microsoft SQL Server 6.5 Service Pack 5a                     | 1998/12/24       | 不适用           | 不适用           |                           |                                                              |
| Microsoft SQL Server 6.5 标准版                              | 1996/6/30        | 2002/1/1         | 不适用           |                           |                                                              |
| Microsoft SQL Server 7.0 Enterprise Edition                  | 1999/3/1         | 2005/12/31       | 2011/1/11        |                           |                                                              |
| Microsoft SQL Server 7.0 Service Pack 1                      | 不适用           | 不适用           | 不适用           |                           |                                                              |
| Microsoft SQL Server 7.0 Service Pack 2                      | 不适用           | 不适用           | 不适用           | 2000/3/20                 |                                                              |
| Microsoft SQL Server 7.0 Service Pack 3                      | 不适用           | 不适用           | 不适用           | 2002/7/26                 |                                                              |
| Microsoft SQL Server 7.0 Service Pack 4                      | 2002/4/26        | 查看注释         | 查看注释         |                           | 支持在下一个服务包发布 12 个月后终止，或是在产品生命周期结束时终止，以较早的日期为准。有关详细信息，请参阅[服务包策略](https://support.microsoft.com/help/17138)。 |
| Microsoft SQL Server 7.0 标准版                              | 1999/3/1         | 2005/12/31       | 2011/1/11        |                           |                                                              |
| Microsoft SQL Server Compact 3.5                             | 2008/2/19        | 不适用           | 不适用           | 2009/10/13                | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| Microsoft SQL Server Compact 3.5 Service Pack 1 for Windows Mobile | 2008/8/11        | 不适用           | 不适用           | 2011/7/12                 |                                                              |
| SQL Server 2008 Developer                                    | 2008/11/6        | 不适用           | 不适用           | 2010/4/13                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 Enterprise                                   | 2008/11/7        | 不适用           | 不适用           | 2010/4/13                 | 可在[此处](https://support.microsoft.com/zh-cn/help/4057281)找到迁移指导。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates)可用于此产品。 有关支持结束日期，请参阅最新的 Service Pack 列表。 |
| SQL Server 2008 Express                                      | 2008/11/11       | 不适用           | 不适用           | 2010/4/13                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 Express with Advanced Services               | 2008/11/22       | 不适用           | 不适用           | 2010/4/13                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 R2 Datacenter                                | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 迁移指导和支持选项可在[这里](https://aka.ms/AA1ovn4)找到。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于此产品。 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。 |
| SQL Server 2008 R2 Developer                                 | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 R2 Enterprise                                | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 可在[此处](https://support.microsoft.com/zh-cn/help/4057281)找到迁移指导。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates)可用于此产品。 有关支持结束日期，请参阅最新的 Service Pack 列表。 |
| SQL Server 2008 R2 Express                                   | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 R2 Express with Advanced Services            | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 R2 Parallel Data Warehouse                   | 2010/11/9        | 2014/7/8         | 2019/7/9         |                           |                                                              |
| SQL Server 2008 R2 Service Pack 3                            | 查看注释         | 2014/7/8         | 2019/7/9         |                           | [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于该产品的企业版、标准版、Web 版、数据中心和工作组版本，并在支持终止后的三年内可使用。前往[迁移指导](https://docs.microsoft.com/zh-cn/sql/sql-server/end-of-support/sql-server-end-of-life-overview)和[支持选项](https://aka.ms/AA1ovn4)。 SQL Server 2008 R2 SP3 的生命周期开始日期为 2014 年 9 月 26 日。 |
| SQL Server 2008 R2 Standard                                  | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 可在[此处](https://support.microsoft.com/zh-cn/help/4057281)找到迁移指导。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates)可用于此产品。 有关支持结束日期，请参阅最新的 Service Pack 列表。 |
| SQL Server 2008 R2 Standard Edition for Small Business       | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 R2 Web                                       | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 迁移指导和支持选项可在[这里](https://aka.ms/AA1ovn4)找到。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于此产品。 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。 |
| SQL Server 2008 R2 Workgroup                                 | 2010/7/20        | 不适用           | 不适用           | 2012/7/10                 | 迁移指导和支持选项可在[这里](https://aka.ms/AA1ovn4)找到。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于此产品。 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。 |
| SQL Server 2008 Service Pack 3                               | 2011/10/6        | 不适用           | 不适用           | 2015/10/13                | 请参阅此产品最新的 Service Pack 列表，了解支持终止日期。仅针对 IA64，SP3 将在 2019 年 7 月 9 日之前受到支持。有关详细信息，请参阅 SQL Release Services 博客，网址为：http://blogs.msdn.com/b/sqlreleaseservices/archive/2014/09/30/sql-server-2008-service-pack-4-has-released.aspx |
| SQL Server 2008 Service Pack 4                               | 2014/7/7         | 2014/7/8         | 2019/7/9         |                           | [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于该产品的企业版、标准版、Web 版、数据中心和工作组版本，并在支持终止后的三年内可使用。前往[迁移指导](https://docs.microsoft.com/zh-cn/sql/sql-server/end-of-support/sql-server-end-of-life-overview)和[支持选项](https://aka.ms/AA1ovn4)。 |
| SQL Server 2008 Standard                                     | 2008/11/6        | 不适用           | 不适用           | 2010/4/13                 | 可在[此处](https://support.microsoft.com/zh-cn/help/4057281)找到迁移指导。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates)可用于此产品。 有关支持结束日期，请参阅最新的 Service Pack 列表。 |
| SQL Server 2008 Standard Edition for Small Business          | 2008/11/6        | 不适用           | 不适用           | 2010/4/13                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。可在[此处](https://aka.ms/AA1ovn4)找到迁移指南和支持选项。 |
| SQL Server 2008 Web                                          | 2008/11/6        | 不适用           | 不适用           | 2010/4/13                 | 迁移指导和支持选项可在[这里](https://aka.ms/AA1ovn4)找到。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于此产品。 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。 |
| SQL Server 2008 Workgroup                                    | 2008/11/6        | 不适用           | 不适用           | 2010/4/13                 | 迁移指导和支持选项可在[这里](https://aka.ms/AA1ovn4)找到。 [扩展安全更新](https://support.microsoft.com/zh-cn/help/4497181/lifecycle-faq-extended-security-updates) (ESU) 可用于此产品。 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。 |
| SQL Server 2012 Business Intelligence                        | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2012 Developer                                    | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2012 Enterprise                                   | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2012 Enterprise Core                              | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。     |
| SQL Server 2012 Express                                      | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2012 Parallel Data Warehouse                      | 2013/7/12        | 2019/10/8        | 2024/10/8        |                           | SQL Server 2012 并行数据仓库 (PDW) 已更名为 APS（分析平台系统）。 |
| SQL Server 2012 Service Pack 4                               | 查看注释         | 2017/7/11        | 2022/7/12        |                           | [SQL Server 2012 SP4](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2012-service-pack-4-sp4-released) 的生命周期开始日期为 2017 年 10 月 5 日。 支持会于发布下一个 Service Pack 的 12 个月后终止，或于产品的支持生命周期结束时终止，以时间先到者为准。有关更多信息，请参阅 [Service Pack 策略](https://support.microsoft.com/zh-cn/help/17138)。 可在[此处](https://docs.microsoft.com/zh-cn/sql/sql-server/end-of-support/sql-server-end-of-life-overview)找到迁移指导。 |
| SQL Server 2012 Standard                                     | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 支持在下一个服务包发布 12 个月后终止，或是在产品生命周期结束时终止，以较早的日期为准。有关详细信息，请参阅[服务包策略](https://support.microsoft.com/help/17138)。 |
| SQL Server 2012 Web                                          | 2012/5/20        | 不适用           | 不适用           | 2014/1/14                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Business Intelligence                        | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Developer                                    | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Enterprise                                   | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Enterprise Core                              | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Express                                      | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Service Pack 2                               | 2016/7/14        | 不适用           | 不适用           | 2020/1/14                 | 有关支持结束日期，请参阅本产品最新的 Service Pack 列表。     |
| SQL Server 2014 Service Pack 3                               | 2018/10/30       | 2019/7/9         | 2024/7/9         |                           | 支持在下一个服务包发布 12 个月后终止，或是在产品支持生命周期结束时终止，以较早的日期为准。有关详细信息，请参阅[服务包策略](https://support.microsoft.com/help/17138)。 |
| SQL Server 2014 Standard                                     | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2014 Web                                          | 2014/6/5         | 不适用           | 不适用           | 2016/7/12                 | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Developer                                    | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Enterprise                                   | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Enterprise Core                              | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Express                                      | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Service Pack 1                               | 2016/11/16       | 不适用           | 不适用           | 2019/7/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Service Pack 2                               | 2018/4/24        | 2021/7/13        | 2026/7/14        |                           | 支持在下一个服务包发布 12 个月后终止，或是在产品生命周期结束时终止，以较早的日期为准。有关详细信息，请参阅[服务包策略](https://support.microsoft.com/help/17138)。 |
| SQL Server 2016 Standard                                     | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server 2016 Web                                          | 2016/6/1         | 不适用           | 不适用           | 2018/1/9                  | 请参阅最新 Service Pack 一览表，了解此产品的终止支持日期。   |
| SQL Server Compact 3.5 Service Pack 2                        | 2010/6/29        | 2013/4/9         | 2018/4/10        |                           | 支持在下一个服务包发布 12 个月后终止，或是在产品生命周期结束时终止，以较早的日期为准。有关详细信息，请参阅[服务包策略](https://support.microsoft.com/help/17138)。 |
| SQL Server Compact 4.0                                       | 2011/4/13        | 2016/7/12        | 2021/7/13        |                           |                                                              |



#### 1.2.3 SQL Server 完整版本列表表格

​	通过访问SQL Server完整版本列表表格，最终确定需要下载的版本。

> **注意** 这些表格使用下列格式并按内部版本号进行排序。



##### SQL Server 2019

| 内部版本号或版本 | Service Pack | 更新       | 知识库文章                                                  | 发布日期            |
| ------------ | ---- | ---- | ----------------------------------------------------------- | ------------------ |
| 15.0.4043.16 | 无   | CU5  | [4552255](https://support.microsoft.com/zh-cn/help/4552255) | 2020 年 6 月 22 日 |
| 15.0.4033.1  | 无   | CU4  | [4548597](https://support.microsoft.com/zh-cn/help/4548597) | 2020 年 3 月 31 日 |
| 15.0.4023.6  | 无   | CU3  | [4538853](https://support.microsoft.com/zh-cn/help/4538853) | 2020 年 3 月 12 日 |
| 15.0.4013.40 | 无   | CU2  | [4536075](https://support.microsoft.com/zh-cn/help/4536075) | 2020 年 2 月 13 日 |
| 15.0.4003.23 | 无   | CU1  | [4527376](https://support.microsoft.com/zh-cn/help/4527376) | 2020 年 1 月 7 日  |
| 15.0.2070.41 | 无   | GDR1 | [4517790](https://support.microsoft.com/zh-cn/help/4517790) | 2019 年 11 月 4 日 |
| 15.0.2000.5  | 无   | RTM  | NA                                                          | 2019 年 11 月 4 日 |



##### SQL Server 2017

| 内部版本号或版本 | Service Pack | 更新       | 知识库文章                                                  | 发布日期            |
| ---------------- | ------------ | ---------- | ----------------------------------------------------------- | ------------------- |
| 14.0.3335.7      | 无           | CU21       | [4557397](https://support.microsoft.com/zh-cn/help/4557397) | 2020 年 7 月 1 日   |
| 14.0.3294.2      | 无           | CU20       | [4541283](https://support.microsoft.com/zh-cn/help/4541283) | 2020 年 4 月 7 日   |
| 14.0.3281.6      | 无           | CU19       | [4535007](https://support.microsoft.com/zh-cn/help/4535007) | 2020 年 2 月 5 日   |
| 14.0.3257.3      | 无           | CU18       | [4527377](https://support.microsoft.com/zh-cn/help/4527377) | 2019 年 12 月 9 日  |
| 14.0.3238.1      | 无           | CU17       | [4515579](https://support.microsoft.com/zh-cn/help/4515579) | 2019 年 10 月 8 日  |
| 14.0.3223.3      | 无           | CU16       | [4508218](https://support.microsoft.com/zh-cn/help/4508218) | 2019 年 8 月 1 日   |
| 14.0.3192.2      | 无           | CU15 + GDR | [4505225](https://support.microsoft.com/zh-cn/help/4505225) | 2019 年 7 月 9 日   |
| 14.0.3162.1      | 无           | CU15       | [4498951](https://support.microsoft.com/zh-cn/help/4498951) | 2019 年 5 月 23 日  |
| 14.0.3103.1      | 无           | CU14 + GDR | [4494352](https://support.microsoft.com/zh-cn/help/4494352) | 2019 年 5 月 14 日  |
| 14.0.3076.1      | 无           | CU14       | [4484710](https://support.microsoft.com/zh-cn/help/4484710) | 2019 年 3 月 25 日  |
| 14.0.3048.4      | 无           | CU13       | [4466404](https://support.microsoft.com/zh-cn/help/4466404) | 2018 年 12 月 18 日 |
| 14.0.3045.24     | 无           | CU12       | [4464082](https://support.microsoft.com/zh-cn/help/4464082) | 2018 年 10 月 24 日 |
| 14.0.3038.14     | 无           | CU11       | [4462262](https://support.microsoft.com/zh-cn/help/4462262) | 2018 年 9 月 20 日  |
| 14.0.3037.1      | 无           | CU10       | [4342123](https://support.microsoft.com/zh-cn/help/4342123) | 2018 年 8 月 27 日  |
| 14.0.3035.2      | 无           | CU9 GDR    | [4293805](https://support.microsoft.com/zh-cn/help/4293805) | 2018 年 8 月 14 日  |
| 14.0.3030.27     | 无           | CU9        | [4341265](https://support.microsoft.com/zh-cn/help/4341265) | 2018 年 7 月 18 日  |
| 14.0.3029.16     | 无           | CU8        | [4338363](https://support.microsoft.com/zh-cn/help/4338363) | 2018 年 6 月 21 日  |
| 14.0.3026.27     | 无           | CU7        | [4229789](https://support.microsoft.com/zh-cn/help/4229789) | 2018 年 5 月 23 日  |
| 14.0.3025.34     | 无           | CU6        | [4101464](https://support.microsoft.com/zh-cn/help/4101464) | 2018 年 4 月 17 日  |
| 14.0.3023.8      | 无           | CU5        | [4092643](https://support.microsoft.com/zh-cn/help/4092643) | 2018 年 3 月 20 日  |
| 14.0.3022.28     | 无           | CU4        | [4056498](https://support.microsoft.com/zh-cn/help/4056498) | 2018 年 2 月 20 日  |
| 14.0.3015.40     | 无           | CU3        | [4052987](https://support.microsoft.com/zh-cn/help/4052987) | 2018 年 1 月 4 日   |
| 14.0.3008.27     | 无           | CU2        | [4052574](https://support.microsoft.com/zh-cn/help/4052574) | 2017 年 11 月 28 日 |
| 14.0.3006.16     | 无           | CU1        | [4038634](https://support.microsoft.com/zh-cn/help/4038634) | 2017 年 10 月 24 日 |



##### SQL Server 2016

| 内部版本号或版本 | Service Pack | 更新            | 知识库文章                                                  | 发布日期            |
| ---------------- | ------------ | --------------- | ----------------------------------------------------------- | ------------------- |
| 13.0.5820.21     | SP2          | CU13            | [4549825](https://support.microsoft.com/zh-cn/help/4549825) | 2020 年 5 月 28 日  |
| 13.0.5698.0      | SP2          | CU12            | [4536648](https://support.microsoft.com/zh-cn/help/4536648) | 2020 年 2 月 25 日  |
| 13.0.5598.27     | SP2          | CU11            | [4527378](https://support.microsoft.com/zh-cn/help/4527378) | 2019 年 12 月 9 日  |
| 13.0.5492.2      | SP2          | CU10            | [4524334](https://support.microsoft.com/zh-cn/help/4524334) | 2019 年 10 月 8 日  |
| 13.0.5426.0      | SP2          | CU8             | [4505830](https://support.microsoft.com/zh-cn/help/4505830) | 2019 年 7 月 31 日  |
| 13.0.5366.0      | SP2          | CU7 + GDR       | [4505222](https://support.microsoft.com/zh-cn/help/4505222) | 2019 年 7 月 9 日   |
| 13.0.5337.0      | SP2          | CU7             | [4495256](https://support.microsoft.com/zh-cn/help/4495256) | 2019 年 5 月 22 日  |
| 13.0.5292.0      | SP2          | CU6             | [4488536](https://support.microsoft.com/zh-cn/help/4488536) | 2019 年 3 月 19 日  |
| 13.0.5264.1      | SP2          | CU5             | [4475776](https://support.microsoft.com/zh-cn/help/4475776) | 2019 年 1 月 23 日  |
| 13.0.5233.0      | SP2          | CU4             | [4464106](https://support.microsoft.com/zh-cn/help/4464106) | 2018 年 11 月 13 日 |
| 13.0.5216.0      | SP2          | CU3             | [4458871](https://support.microsoft.com/zh-cn/help/4458871) | 2018 年 9 月 20 日  |
| 13.0.5201.2      | SP2          | CU2 + 安全更新  | [4458621](https://support.microsoft.com/zh-cn/help/4458621) | 2018 年 8 月 21 日  |
| 13.0.5153.0      | SP2          | CU2             | [4340355](https://support.microsoft.com/zh-cn/help/4340355) | 2018 年 7 月 16 日  |
| 13.0.5149.0      | SP2          | CU1             | [4135048](https://support.microsoft.com/zh-cn/help/4135048) | 2018 年 5 月 30 日  |
| 13.0.5026.0      | SP2          | RTW/PCU2        | [4052908](https://support.microsoft.com/zh-cn/help/4052908) | 2018 年 4 月 24 日  |
| 13.0.4604.0      | SP1          | CU15 + GDR      | [4505221](https://support.microsoft.com/zh-cn/help/4505221) | 2019 年 7 月 9 日   |
| 13.0.4574.0      | SP1          | CU15            | [4495257](https://support.microsoft.com/zh-cn/help/4495257) | 2019 年 5 月 16 日  |
| 13.0.4560.0      | SP1          | CU14            | [4488535](https://support.microsoft.com/zh-cn/help/4488535) | 2019 年 3 月 19 日  |
| 13.0.4550.1      | SP1          | CU13            | [4475775](https://support.microsoft.com/zh-cn/help/4475775) | 2019 年 1 月 23 日  |
| 13.0.4541.0      | SP1          | CU12            | [4464343](https://support.microsoft.com/zh-cn/help/4464343) | 2018 年 11 月 13 日 |
| 13.0.4528.0      | SP1          | CU11            | [4459676](https://support.microsoft.com/zh-cn/help/4459676) | 2018 年 9 月 17 日  |
| 13.0.4224.16     | SP1          | CU10 + 安全更新 | [4458842](https://support.microsoft.com/zh-cn/help/4458842) | 2018 年 8 月 22 日  |
| 13.0.4514.0      | SP1          | CU10            | [4341569](https://support.microsoft.com/zh-cn/help/4341569) | 2018 年 7 月 16 日  |
| 13.0.4502.0      | SP1          | CU9             | [4100997](https://support.microsoft.com/zh-cn/help/4100997) | 2018 年 5 月 30 日  |
| 13.0.4474.0      | SP1          | CU8             | [4077064](https://support.microsoft.com/zh-cn/help/4077064) | 2018 年 3 月 19 日  |
| 13.0.4466.4      | SP1          | CU7             | [4057119](https://support.microsoft.com/zh-cn/help/4057119) | 2018 年 1 月 4 日   |
| 13.0.4457.0      | SP1          | CU6             | [4037354](https://support.microsoft.com/zh-cn/help/4037354) | 2017 年 11 月 20 日 |
| 13.0.4451.0      | SP1          | CU5             | [4040714](https://support.microsoft.com/zh-cn/help/4040714) | 2017 年 9 月 18 日  |
| 13.0.4446.0      | SP1          | CU4             | [4024305](https://support.microsoft.com/zh-cn/help/4024305) | 2017 年 8 月 8 日   |
| 13.0.4435.0      | SP1          | CU3             | [4019916](https://support.microsoft.com/zh-cn/help/4019916) | 2017 年 5 月 15 日  |
| 13.0.4422.0      | SP1          | CU2             | [4013106](https://support.microsoft.com/zh-cn/help/4013106) | 2017 年 3 月 20 日  |
| 13.0.4411.0      | SP1          | CU1             | [3208177](https://support.microsoft.com/zh-cn/help/3208177) | 2017 年 1 月 17 日  |
| 13.0.4001.0      | SP1          | RTW/PCU1        | [3182545](https://support.microsoft.com/zh-cn/help/3182545) | 2016 年 11 月 16 日 |
| 13.0.2216.0      | RTM          | CU9             | [4037357](https://support.microsoft.com/zh-cn/help/4037357) | 2017 年 11 月 20 日 |
| 13.0.2213.0      | RTM          | CU8             | [4040713](https://support.microsoft.com/zh-cn/help/4040713) | 2017 年 9 月 18 日  |
| 13.0.2210.0      | RTM          | CU7             | [4024304](https://support.microsoft.com/zh-cn/help/4024304) | 2017 年 8 月 8 日   |
| 13.0.2204.0      | RTM          | CU6             | [4019914](https://support.microsoft.com/zh-cn/help/4019914) | 2017 年 5 月 15 日  |
| 13.0.2197.0      | RTM          | CU5             | [4013105](https://support.microsoft.com/zh-cn/help/4013105) | 2017 年 3 月 20 日  |
| 13.0.2193.0      | RTM          | CU4             | [3205052](https://support.microsoft.com/zh-cn/help/3205052) | 2017 年 1 月 17 日  |
| 13.0.2186.6      | RTM          | CU3             | [3205413](https://support.microsoft.com/zh-cn/help/3205413) | 2016 年 11 月 16 日 |
| 13.0.2164.0      | RTM          | CU2             | [3182270](https://support.microsoft.com/zh-cn/help/3182270) | 2016 年 9 月 22 日  |
| 13.0.2149.0      | RTM          | CU1             | [3164674](https://support.microsoft.com/zh-cn/help/3164674) | 2016 年 7 月 25 日  |



##### SQL Server 2014

| 内部版本号或版本 | Service Pack | 更新                    | 知识库文章                                                  | 发布日期            |
| ---------------- | ------------ | ----------------------- | ----------------------------------------------------------- | ------------------- |
| 12.0.6329.1      | SP3          | CU4                     | [4500181](https://support.microsoft.com/zh-cn/help/4500181) | 2019 年 7 月 29 日  |
| 12.0.6293.0      | SP3          | CU3 + GDR               | [4505422](https://support.microsoft.com/zh-cn/help/4505422) | 2019 年 7 月 9 日   |
| 12.0.6259.0      | SP3          | CU3                     | [4491539](https://support.microsoft.com/zh-cn/help/4491539) | 2019 年 4 月 16 日  |
| 12.0.6214.1      | SP3          | CU2                     | [4482960](https://support.microsoft.com/zh-cn/help/4482960) | 2019 年 2 月 19 日  |
| 12.0.6205.1      | SP3          | CU1                     | [4470220](https://support.microsoft.com/zh-cn/help/4470220) | 2018 年 12 月 12 日 |
| 12.0.6024.0      | SP3          | RTW/PCU3                | [4022619](https://support.microsoft.com/zh-cn/help/4022619) | 2018 年 10 月 30 日 |
| 12.0.5687.1      | SP2          | CU18                    | [4500180](https://support.microsoft.com/zh-cn/help/4500180) | 2019 年 7 月 29 日  |
| 12.0.5659.1      | SP2          | CU17 + GDR              | [4505419](https://support.microsoft.com/zh-cn/help/4505419) | 2019 年 7 月 9 日   |
| 12.0.5632.1      | SP2          | CU17                    | [4491540](https://support.microsoft.com/zh-cn/help/4491540) | 2019 年 4 月 16 日  |
| 12.0.5626.1      | SP2          | CU16                    | [4482967](https://support.microsoft.com/zh-cn/help/4482967) | 2019 年 2 月 19 日  |
| 12.0.5605.1      | SP2          | CU15                    | [4469137](https://support.microsoft.com/zh-cn/help/4469137) | 2018 年 12 月 12 日 |
| 12.0.5600.1      | SP2          | CU14                    | [4459860](https://support.microsoft.com/zh-cn/help/4459860) | 2018 年10 月 15 日  |
| 12.0.5590.1      | SP2          | CU13                    | [4456287](https://support.microsoft.com/zh-cn/help/4456287) | 2018 年 8 月 27 日  |
| 12.0.5589.7      | SP2          | CU12                    | [4130489](https://support.microsoft.com/zh-cn/help/4130489) | 2018 年 6 月 18 日  |
| 12.0.5579.0      | SP2          | CU11                    | [4077063](https://support.microsoft.com/zh-cn/help/4077063) | 2018 年 3 月 19 日  |
| 12.0.5571.0      | SP2          | CU10                    | [4052725](https://support.microsoft.com/zh-cn/help/4052725) | 2018 年 1 月 16 日  |
| 12.0.5563.0      | SP2          | CU9                     | [4055557](https://support.microsoft.com/zh-cn/help/4055557) | 2017 年 12 月 18 日 |
| 12.0.5557.0      | SP2          | CU8                     | [4037356](https://support.microsoft.com/zh-cn/help/4037356) | 2017 年 10 月 16 日 |
| 12.0.5556.0      | SP2          | CU7                     | [4032541](https://support.microsoft.com/zh-cn/help/4032541) | 2017 年 8 月 28 日  |
| 12.0.5553.0      | SP2          | CU6                     | [4019094](https://support.microsoft.com/zh-cn/help/4019094) | 2017 年 8 月 8 日   |
| 12.0.5546.0      | SP2          | CU5                     | [4013098](https://support.microsoft.com/zh-cn/help/4013098) | 2017 年 4 月 17 日  |
| 12.0.5540.0      | SP2          | CU4                     | [4010394](https://support.microsoft.com/zh-cn/help/4010394) | 2017 年 2 月 21 日  |
| 12.0.5538.0      | SP2          | CU3                     | [3204388](https://support.microsoft.com/zh-cn/help/3204388) | 2016 年 12 月 19 日 |
| 12.0.5522.0      | SP2          | CU2                     | [3188778](https://support.microsoft.com/zh-cn/help/3188778) | 2016 年 10 月 17 日 |
| 12.0.5511.0      | SP2          | CU1                     | [3178925](https://support.microsoft.com/zh-cn/help/3178925) | 2016 年 8 月 25 日  |
| 12.0.5000.0      | SP2          | RTW/PCU2                | [3171021](https://support.microsoft.com/zh-cn/help/3171021) | 2016 年 7 月 11 日  |
| 12.0.4522.0      | SP1          | CU13                    | [4019099](https://support.microsoft.com/zh-cn/help/4019099) | 2017 年 8 月 8 日   |
| 12.0.4511.0      | SP1          | CU12                    | [4017793](https://support.microsoft.com/zh-cn/help/4017793) | 2017 年 4 月 17 日  |
| 12.0.4502.0      | SP1          | CU11                    | [4010392](https://support.microsoft.com/zh-cn/help/4010392) | 2017 年 2 月 21 日  |
| 12.0.4491.0      | SP1          | CU10                    | [3204399](https://support.microsoft.com/zh-cn/help/3204399) | 2016 年 12 月 19 日 |
| 12.0.4474.0      | SP1          | CU9                     | [3186964](https://support.microsoft.com/zh-cn/help/3186964) | 2016 年 10 月 17 日 |
| 12.0.4468.0      | SP1          | CU8                     | [3174038](https://support.microsoft.com/zh-cn/help/3174038) | 2016 年 8 月 15 日  |
| 12.0.4459.0      | SP1          | CU7                     | [3162659](https://support.microsoft.com/zh-cn/help/3162659) | 2016 年 6 月 20 日  |
| 12.0.4457.0      | SP1          | CU6                     | [3167392](https://support.microsoft.com/zh-cn/help/3167392) | 2016 月 5 月 30 日  |
| 12.0.4449.0      | SP1          | CU6                     | [3144524](https://support.microsoft.com/zh-cn/help/3144524) | 2016 年 4 月 18 日  |
| 12.0.4438.0      | SP1          | CU5                     | [3130926](https://support.microsoft.com/zh-cn/help/3130926) | 2016 年 2 月 22 日  |
| 12.0.4436.0      | SP1          | CU4                     | [3106660](https://support.microsoft.com/zh-cn/help/3106660) | 2015 年 12 月 21 日 |
| 12.0.4427.24     | SP1          | CU3                     | [3094221](https://support.microsoft.com/zh-cn/help/3094221) | 2015 年 10 月 19 日 |
| 12.0.4422.0      | SP1          | CU2                     | [3075950](https://support.microsoft.com/zh-cn/help/3075950) | 2015 年 8 月 17 日  |
| 12.0.4416.0      | SP1          | CU1                     | [3067839](https://support.microsoft.com/zh-cn/help/3067839) | 2015 年 6 月 19 日  |
| 12.0.4213.0      | SP1          | MS15-058： GDR 安全更新 | [3070446](https://support.microsoft.com/zh-cn/help/3070446) | 2015 年 7 月 14 日  |
| 12.0.4100.1      | SP1          | RTW/PCU1                | [3058865](https://support.microsoft.com/zh-cn/help/3058865) | 2015 年 5 月 4 日   |
| 12.0.2569.0      | RTM          | CU14                    | [3158271](https://support.microsoft.com/zh-cn/help/3158271) | 2016 年 6 月 20 日  |
| 12.0.2568.0      | RTM          | CU13                    | [3144517](https://support.microsoft.com/zh-cn/help/3144517) | 2016 年 4 月 18 日  |
| 12.0.2564.0      | RTM          | CU12                    | [3130923](https://support.microsoft.com/zh-cn/help/3130923) | 2016 年 2 月 22 日  |
| 12.0.2560.0      | RTM          | CU11                    | [3106659](https://support.microsoft.com/zh-cn/help/3106659) | 2015 年 12 月 21 日 |
| 12.0.2556.4      | RTM          | CU10                    | [3094220](https://support.microsoft.com/zh-cn/help/3094220) | 2015 年 10 月 19 日 |
| 12.0.2553.0      | RTM          | CU9                     | [3075949](https://support.microsoft.com/zh-cn/help/3075949) | 2015 年 8 月 17 日  |
| 12.0.2548.0      | RTM          | MS15-058： QFE 安全更新 | [3045323](https://support.microsoft.com/zh-cn/help/3045323) | 2015 年 7 月 14 日  |
| 12.0.2546.0      | RTM          | CU8                     | [3067836](https://support.microsoft.com/zh-cn/help/3067836) | 2015 年 6 月 19 日  |
| 12.0.2495.0      | RTM          | CU7                     | [3046038](https://support.microsoft.com/zh-cn/help/3046038) | 2015 年 4 月 20 日  |
| 12.0.2480.0      | RTM          | CU6                     | [3031047](https://support.microsoft.com/zh-cn/help/3031047) | 2015 年 2 月 16 日  |
| 12.0.2456.0      | RTM          | CU5                     | [3011055](https://support.microsoft.com/zh-cn/help/3011055) | 2014 年 12 月 17 日 |
| 12.0.2430.0      | RTM          | CU4                     | [2999197](https://support.microsoft.com/zh-cn/help/2999197) | 2014 年 10 月 21 日 |
| 12.0.2402.0      | RTM          | CU3                     | [2984923](https://support.microsoft.com/zh-cn/help/2984923) | 2014 年 8 月 18 日  |
| 12.0.2381.0      | RTM          | MS14-044： QFE 安全更新 | [2977316](https://support.microsoft.com/zh-cn/help/2977316) | 2014 年 8 月 12 日  |
| 12.0.2370.0      | RTM          | CU2                     | [2967546](https://support.microsoft.com/zh-cn/help/2967546) | 2014 年 6 月 27 日  |
| 12.0.2342.0      | RTM          | CU1                     | [2931693](https://support.microsoft.com/zh-cn/help/2931693) | 2014 年 4 月 21 日  |
| 12.0.2269.0      | RTM          | MS15-058： GDR 安全更新 | [3045324](https://support.microsoft.com/zh-cn/help/3045324) | 2015 年 7 月 14 日  |
| 12.0.2254.0      | RTM          | MS14-044： GDR 安全更新 | [2977315](https://support.microsoft.com/zh-cn/help/2977315) | 2014 年 8 月 12 日  |
| 12.0.2000.8      | RTM          |                         |                                                             | 2014 年 4 月 1 日   |



##### SQL Server 2012

| 内部版本号或版本 | Service Pack | 更新                    | 知识库文章                                                  | 发布日期            |
| ---------------- | ------------ | ----------------------- | ----------------------------------------------------------- | ------------------- |
| 11.0.7001.0      | SP4          | RTW/PCU4                | [4018073](https://support.microsoft.com/zh-cn/help/4018073) | 2017 年 10 月 2 日  |
| 11.0.6607.3      | SP3          | CU10                    | [4025925](https://support.microsoft.com/zh-cn/help/4025925) | 2017 年 8 月 8 日   |
| 11.0.6598.0      | SP3          | CU9                     | [4016762](https://support.microsoft.com/zh-cn/help/4016762) | 2017 年 5 月 15 日  |
| 11.0.6594.0      | SP3          | CU8                     | [4013104](https://support.microsoft.com/zh-cn/help/4013104) | 2017 年 3 月 20 日  |
| 11.0.6579.0      | SP3          | CU7                     | [3205051](https://support.microsoft.com/zh-cn/help/3205051) | 2017 年 1 月 17 日  |
| 11.0.6567.0      | SP3          | CU6                     | [3194992](https://support.microsoft.com/zh-cn/help/3194992) | 2016 年 11 月 17 日 |
| 11.0.6248.0      | SP3          | MS16-136 GDR 安全更新   | [3194721](https://support.microsoft.com/zh-cn/help/3194721) | 2016 年 11 月 8 日  |
| 11.0.6544.0      | SP3          | CU5                     | [3180915](https://support.microsoft.com/zh-cn/help/3180915) | 2016 年 9 月 19 日  |
| 11.0.6540.0      | SP3          | CU4                     | [3165264](https://support.microsoft.com/zh-cn/help/3165264) | 2016 年 7 月 18 日  |
| 11.0.6537.0      | SP3          | CU3                     | [3152635](https://support.microsoft.com/zh-cn/help/3152635) | 2016 年 5 月 16 日  |
| 11.0.6523.0      | SP3          | CU2                     | [3137746](https://support.microsoft.com/zh-cn/help/3137746) | 2016 年 3 月 21 日  |
| 11.0.6518.0      | SP3          | CU1                     | [3123299](https://support.microsoft.com/zh-cn/help/3123299) | 2016 年 1 月 19 日  |
| 11.0.6020.0      | SP3          | RTW/PCU3                | [3072779](https://support.microsoft.com/zh-cn/help/3072779) | 2015 年 11 月 20 日 |
| 11.0.5678.0      | SP2          | CU16                    | [3205054](https://support.microsoft.com/zh-cn/help/3205054) | 2016 年 11 月 17 日 |
| 11.0.5676.0      | SP2          | CU15                    | [3205416](https://support.microsoft.com/zh-cn/help/3205416) | 2016 年 11 月 17 日 |
| 11.0.5657.0      | SP2          | CU14                    | [3180914](https://support.microsoft.com/zh-cn/help/3180914) | 2016 年 9 月 19 日  |
| 11.0.5655.0      | SP2          | CU13                    | [3165266](https://support.microsoft.com/zh-cn/help/3165266) | 2016 年 7 月 18 日  |
| 11.0.5649.0      | SP2          | CU12                    | [3152637](https://support.microsoft.com/zh-cn/help/3152637) | 2016 年 5 月 16 日  |
| 11.0.5646.0      | SP2          | CU11                    | [3137745](https://support.microsoft.com/zh-cn/help/3137745) | 2016 年 3 月 21 日  |
| 11.0.5644.2      | SP2          | CU10                    | [3120313](https://support.microsoft.com/zh-cn/help/3120313) | 2016 年 1 月 19 日  |
| 11.0.5641.0      | SP2          | CU9                     | [3098512](https://support.microsoft.com/zh-cn/help/3098512) | 2015 年 11 月 16 日 |
| 11.0.5634.1      | SP2          | CU8                     | [3082561](https://support.microsoft.com/zh-cn/help/3082561) | 2015 年 9 月 21 日  |
| 11.0.5623.0      | SP2          | CU7                     | [3072100](https://support.microsoft.com/zh-cn/help/3072100) | 2015 年 7 月 20 日  |
| 11.0.5613.0      | SP2          | MS15-058： QFE 安全更新 | [3045319](https://support.microsoft.com/zh-cn/help/3045319) | 2015 年 7 月 14 日  |
| 11.0.5592.0      | SP2          | CU6                     | [3052468](https://support.microsoft.com/zh-cn/help/3052468) | 2015 年 5 月 18 日  |
| 11.0.5582.0      | SP2          | CU5                     | [3037255](https://support.microsoft.com/zh-cn/help/3037255) | 2015 年 3 月 16 日  |
| 11.0.5569.0      | SP2          | CU4                     | [3007556](https://support.microsoft.com/zh-cn/help/3007556) | 2015 年 1 月 19 日  |
| 11.0.5556.0      | SP2          | CU3                     | [3002049](https://support.microsoft.com/zh-cn/help/3002049) | 2014 年 11 月 17 日 |
| 11.0.5548.0      | SP2          | CU2                     | [2983175](https://support.microsoft.com/zh-cn/help/2983175) | 2014 年 9 月 15 日  |
| 11.0.5532.0      | SP2          | CU1                     | [2976982](https://support.microsoft.com/zh-cn/help/2976982) | 2014 年 7 月 23 日  |
| 11.0.5343.0      | SP2          | MS15-058： GDR 安全更新 | [3045321](https://support.microsoft.com/zh-cn/help/3045321) | 2015 年 7 月 14 日  |
| 11.0.5058.0      | SP2          | RTW/PCU2                | [2958429](https://support.microsoft.com/zh-cn/help/2958429) | 2014 年 6 月 10 日  |
| 11.0.3513.0      | SP1          | MS15-058： QFE 安全更新 | [3045317](https://support.microsoft.com/zh-cn/help/3045317) | 2015 年 7 月 14 日  |
| 11.0.3482.00     | SP1          | CU13                    | [3002044](https://support.microsoft.com/zh-cn/help/3002044) | 2014 年 11 月 17 日 |
| 11.0.3470.00     | SP1          | CU12                    | [2991533](https://support.microsoft.com/zh-cn/help/2991533) | 2014 年 9 月 15 日  |
| 11.0.3460.0      | SP1          | MS14-044： QFE 安全更新 | [2977325](https://support.microsoft.com/zh-cn/help/2977325) | 2014 年 8 月 12 日  |
| 11.0.3449.00     | SP1          | CU11                    | [2975396](https://support.microsoft.com/zh-cn/help/2975396) | 2014 年 7 月 21 日  |
| 11.0.3431.00     | SP1          | CU10                    | [2954099](https://support.microsoft.com/zh-cn/help/2954099) | 2014 年 5 月 19 日  |
| 11.0.3412.00     | SP1          | CU9                     | [2931078](https://support.microsoft.com/zh-cn/help/2931078) | 2014 年 3 月 17 日  |
| 11.0.3401.00     | SP1          | CU8                     | [2917531](https://support.microsoft.com/zh-cn/help/2917531) | 2014 年 1 月 20 日  |
| 11.0.3393.00     | SP1          | CU7                     | [2894115](https://support.microsoft.com/zh-cn/help/2894115) | 2013 年 11 月 18 日 |
| 11.0.3381.00     | SP1          | CU6                     | [2874879](https://support.microsoft.com/zh-cn/help/2874879) | 2013 年 9 月 16 日  |
| 11.0.3373.00     | SP1          | CU5                     | [2861107](https://support.microsoft.com/zh-cn/help/2861107) | 2013 年 7 月 15 日  |
| 11.0.3368.00     | SP1          | CU4                     | [2833645](https://support.microsoft.com/zh-cn/help/2833645) | 2013 年 5 月 30 日  |
| 11.0.3349.00     | SP1          | CU3                     | [2812412](https://support.microsoft.com/zh-cn/help/2812412) | 2013 年 3 月 18 日  |
| 11.0.3339.00     | SP1          | CU2                     | [2790947](https://support.microsoft.com/zh-cn/help/2790947) | 2013 年 1 月 21 日  |
| 11.0.3321.00     | SP1          | CU1                     | [2765331](https://support.microsoft.com/zh-cn/help/2765331) | 2012 年 11 月 20 日 |
| 11.0.3156.00     | SP1          | MS15-058： GDR 安全更新 | [3045318](https://support.microsoft.com/zh-cn/help/3045318) | 2015 年 7 月 14 日  |
| 11.0.3153.00     | SP1          | MS14-044： GDR 安全更新 | [2977326](https://support.microsoft.com/zh-cn/help/2977326) | 2014 年 8 月 12 日  |
| 11.0.3000.00     | SP1          | RTW/PCU1                | [2674319](https://support.microsoft.com/zh-cn/help/2674319) | 2012 年 11 月 7 日  |
| 11.0.2424.00     | RTM          | CU11                    | [2908007](https://support.microsoft.com/zh-cn/help/2908007) | 2013 年 12 月 16 日 |
| 11.0.2420.00     | RTM          | CU10                    | [2891666](https://support.microsoft.com/zh-cn/help/2891666) | 2013 年 10 月 21 日 |
| 11.0.2419.00     | RTM          | CU9                     | [2867319](https://support.microsoft.com/zh-cn/help/2867319) | 2013 年 8 月 20 日  |
| 11.0.2410.00     | RTM          | CU8                     | [2844205](https://support.microsoft.com/zh-cn/help/2844205) | 2013 年 6 月 17 日  |
| 11.0.2405.00     | RTM          | CU7                     | [2823247](https://support.microsoft.com/zh-cn/help/2823247) | 2013 年 4 月 15 日  |
| 11.0.2401.00     | RTM          | CU6                     | [2728897](https://support.microsoft.com/zh-cn/help/2728897) | 2013 年 2 月 18 日  |
| 11.0.2395.00     | RTM          | CU5                     | [2777772](https://support.microsoft.com/zh-cn/help/2777772) | 2012 年 12 月 17 日 |
| 11.0.2383.00     | RTM          | CU4                     | [2758687](https://support.microsoft.com/zh-cn/help/2758687) | 2012 年 10 月 15 日 |
| 11.0.2376.00     | RTM          | MS12-070： QFE 安全更新 | [2716441](https://support.microsoft.com/zh-cn/help/2716441) | 2012 年 10 月 9 日  |
| 11.0.2332.00     | RTM          | CU3                     | [2723749](https://support.microsoft.com/zh-cn/help/2723749) | 2012 年 8 月 31 日  |
| 11.0.2325.00     | RTM          | CU2                     | [2703275](https://support.microsoft.com/zh-cn/help/2703275) | 2012 年 6 月 18 日  |
| 11.0.2316.00     | RTM          | CU1                     | [2679368](https://support.microsoft.com/zh-cn/help/2679368) | 2012 年 4 月 12 日  |
| 11.0.2218.00     | RTM          | MS12-070： GDR 安全更新 | [2716442](https://support.microsoft.com/zh-cn/help/2716442) | 2012 年 10 月 9 日  |
| 11.0.2100.60     | RTM          |                         |                                                             | 2012 年 3 月 6 日   |



##### SQL Server 2008 R2

| 版本号或版本  | Service Pack | 更新                    | 知识库文章                                                  | 发布日期            |
| ------------- | ------------ | ----------------------- | ----------------------------------------------------------- | ------------------- |
| 10.50.6529.00 | SP3          | MS15-058： QFE 安全更新 | [3045314](https://support.microsoft.com/zh-cn/help/3045314) | 2015 年 7 月 14 日  |
| 10.50.6220.00 | SP3          | MS15-058： QFE 安全更新 | [3045316](https://support.microsoft.com/zh-cn/help/3045316) | 2015 年 7 月 14 日  |
| 10.50.6000.34 | SP3          | RTW/PCU3                | [2979597](https://support.microsoft.com/zh-cn/help/2979597) | 2014 年 9 月 26 日  |
| 10.50.4339.00 | SP2          | MS15-058： QFE 安全更新 | [3045312](https://support.microsoft.com/zh-cn/help/3045312) | 2015 年 7 月 14 日  |
| 10.50.4321.00 | SP2          | MS14-044： QFE 安全更新 | [2977319](https://support.microsoft.com/zh-cn/help/2977319) | 2014 年 8 月 14 日  |
| 10.50.4319.00 | SP2          | CU13                    | [2967540](https://support.microsoft.com/zh-cn/help/2967540) | 2014 年 6 月 30 日  |
| 10.50.4305.00 | SP2          | CU12                    | [2938478](https://support.microsoft.com/zh-cn/help/2938478) | 2014 年 4 月 21 日  |
| 10.50.4302.00 | SP2          | CU11                    | [2926028](https://support.microsoft.com/zh-cn/help/2926028) | 2014 年 2 月 18 日  |
| 10.50.4297.00 | SP2          | CU10                    | [2908087](https://support.microsoft.com/zh-cn/help/2908087) | 2013 年 12 月 17 日 |
| 10.50.4295.00 | SP2          | CU9                     | [2887606](https://support.microsoft.com/zh-cn/help/2887606) | 2013 年 10 月 28 日 |
| 10.50.4290.00 | SP2          | CU8                     | [2871401](https://support.microsoft.com/zh-cn/help/2871401) | 2013 年 8 月 22 日  |
| 10.50.4285.00 | SP2          | CU7                     | [2844090](https://support.microsoft.com/zh-cn/help/2844090) | 2013 年 6 月 17 日  |
| 10.50.4279.00 | SP2          | CU6                     | [2830140](https://support.microsoft.com/zh-cn/help/2830140) | 2013 年 4 月 15 日  |
| 10.50.4276.00 | SP2          | CU5                     | [2797460](https://support.microsoft.com/zh-cn/help/2797460) | 2013 年 2 月 18 日  |
| 10.50.4270.00 | SP2          | CU4                     | [2777358](https://support.microsoft.com/zh-cn/help/2777358) | 2012 年 12 月 17 日 |
| 10.50.4266.00 | SP2          | CU3                     | [2754552](https://support.microsoft.com/zh-cn/help/2754552) | 2012 年 10 月 15 日 |
| 10.50.4263.00 | SP2          | CU2                     | [2740411](https://support.microsoft.com/zh-cn/help/2740411) | 2012 年 8 月 31 日  |
| 10.50.4260.00 | SP2          | CU1                     | [2720425](https://support.microsoft.com/zh-cn/help/2720425) | 2012 年 7 月 24 日  |
| 10.50.4042.00 | SP2          | MS15-058： GDR 安全更新 | [3045313](https://support.microsoft.com/zh-cn/help/3045313) | 2015 年 7 月 14 日  |
| 10.50.4033.00 | SP2          | MS14-044： GDR 安全更新 | [2977320](https://support.microsoft.com/zh-cn/help/2977320) | 2014 年 8 月 12 日  |
| 10.50.4000.0  | SP2          | RTW/PCU2                | [2630458](https://support.microsoft.com/zh-cn/help/2630458) | 2012 年 7 月 26 日  |
| 10.50.2881.00 | SP1          | CU14                    | [2868244](https://support.microsoft.com/zh-cn/help/2868244) | 2013 年 8 月 8 日   |
| 10.50.2876.00 | SP1          | CU13                    | [2855792](https://support.microsoft.com/zh-cn/help/2855792) | 2013 年 6 月 17 日  |
| 10.50.2874.00 | SP1          | CU12                    | [2828727](https://support.microsoft.com/zh-cn/help/2828727) | 2013 年 4 月 15 日  |
| 10.50.2869.00 | SP1          | CU11                    | [2812683](https://support.microsoft.com/zh-cn/help/2812683) | 2013 年 2 月 18 日  |
| 10.50.2868.00 | SP1          | CU10                    | [2783135](https://support.microsoft.com/zh-cn/help/2783135) | 2012 年 12 月 17 日 |
| 10.50.2866.00 | SP1          | CU9                     | [2756574](https://support.microsoft.com/zh-cn/help/2756574) | 2012 年 10 月 15 日 |
| 10.50.2861.00 | SP1          | MS12-070： QFE 安全更新 | [2716439](https://support.microsoft.com/zh-cn/help/2716439) | 2012 年 10 月 9 日  |
| 10.50.2822.00 | SP1          | CU8                     | [2723743](https://support.microsoft.com/zh-cn/help/2723743) | 2012 年 8 月 31 日  |
| 10.50.2817.00 | SP1          | CU7                     | [2703282](https://support.microsoft.com/zh-cn/help/2703282) | 2012 年 6 月 18 日  |
| 10.50.2811.00 | SP1          | CU6                     | [2679367](https://support.microsoft.com/zh-cn/help/2679367) | 2012 年 4 月 16 日  |
| 10.50.2806.00 | SP1          | CU5                     | [2659694](https://support.microsoft.com/zh-cn/help/2659694) | 2012 年 2 月 22 日  |
| 10.50.2796.00 | SP1          | CU4                     | [2633146](https://support.microsoft.com/zh-cn/help/2633146) | 2011 年 12 月 19 日 |
| 10.50.2789.00 | SP1          | CU3                     | [2591748](https://support.microsoft.com/zh-cn/help/2591748) | 2011 年 10 月 17 日 |
| 10.50.2772.00 | SP1          | CU2                     | [2567714](https://support.microsoft.com/zh-cn/help/2567714) | 2011 年 8 月 15 日  |
| 10.50.2769.00 | SP1          | CU1                     | [2544793](https://support.microsoft.com/zh-cn/help/2544793) | 2011 年 7 月 18 日  |
| 10.50.2550.00 | SP1          | MS12-070： GDR 安全更新 | [2754849](https://support.microsoft.com/zh-cn/help/2754849) | 2012 年 10 月 9 日  |
| 10.50.2500.0  | SP1          | RTW/PCU1                | [2528583](https://support.microsoft.com/zh-cn/help/2528583) | 2011 年 7 月 12 日  |
| 10.50.1815.00 | RTM          | CU13                    | [2679366](https://support.microsoft.com/zh-cn/help/2679366) | 2012 年 4 月 16 日  |
| 10.50.1810.00 | RTM          | CU12                    | [2659692](https://support.microsoft.com/zh-cn/help/2659692) | 2012 年 2 月 21 日  |
| 10.50.1809.00 | RTM          | CU11                    | [2633145](https://support.microsoft.com/zh-cn/help/2633145) | 2011 年 12 月 19 日 |
| 10.50.1807.00 | RTM          | CU10                    | [2591746](https://support.microsoft.com/zh-cn/help/2591746) | 2011 年 10 月 17 日 |
| 10.50.1804.00 | RTM          | CU9                     | [2567713](https://support.microsoft.com/zh-cn/help/2567713) | 2011 年 8 月 15 日  |
| 10.50.1797.00 | RTM          | CU8                     | [2534352](https://support.microsoft.com/zh-cn/help/2534352) | 2011 年 6 月 20 日  |
| 10.50.1790.00 | RTM          | MS11-049： QFE 安全更新 | [2494086](https://support.microsoft.com/zh-cn/help/2494086) | 2011 年 6 月 14 日  |
| 10.50.1777.00 | RTM          | CU7                     | [2507770](https://support.microsoft.com/zh-cn/help/2507770) | 2011 年 4 月 18 日  |
| 10.50.1765.00 | RTM          | CU6                     | [2489376](https://support.microsoft.com/zh-cn/help/2489376) | 2011 年 2 月 21 日  |
| 10.50.1753.00 | RTM          | CU5                     | [2438347](https://support.microsoft.com/zh-cn/help/2438347) | 2010 年 12 月 20 日 |
| 10.50.1746.00 | RTM          | CU4                     | [2345451](https://support.microsoft.com/zh-cn/help/2345451) | 2010 年 10 月 18 日 |
| 10.50.1734.00 | RTM          | CU3                     | [2261464](https://support.microsoft.com/zh-cn/help/2261464) | 2010 年 8 月 16 日  |
| 10.50.1720.00 | RTM          | CU2                     | [2072493](https://support.microsoft.com/zh-cn/help/2072493) | 2010 年 6 月 21 日  |
| 10.50.1702.00 | RTM          | CU1                     | [981355](https://support.microsoft.com/zh-cn/help/981355)   | 2010 年 5 月 18 日  |
| 10.50.1617.00 | RTM          | MS11-049： GDR 安全更新 | [2494088](https://support.microsoft.com/zh-cn/help/2494088) | 2011 年 6 月 14 日  |
| 10.50.1600.1  | RTM          |                         |                                                             | 2010 年 5 月 10 日  |



##### SQL Server 2008

| 内部版本号或版本 | Service Pack   | 更新                    | 知识库文章                                                   | 发布日期            |
| ---------------- | -------------- | ----------------------- | ------------------------------------------------------------ | ------------------- |
| 10.00.6535.00    | SP3            | MS15-058： QFE 安全更新 | [3045308](https://support.microsoft.com/zh-cn/help/3045308)  | 2015 年 7 月 14 日  |
| 10.00.6241.00    | SP3            | MS15-058： GDR 安全更新 | [3045311](https://support.microsoft.com/zh-cn/help/3045311)  | 2015 年 7 月 14 日  |
| 10.00.5890.00    | SP3            | MS15-058： QFE 安全更新 | [3045303](https://support.microsoft.com/zh-cn/help/3045303)  | 2015 年 7 月 14 日  |
| 10.00.5869.00    | SP3            | MS14-044： QFE 安全更新 | [2984340](https://support.microsoft.com/zh-cn/help/2984340)、[2977322](https://support.microsoft.com/zh-cn/help/2977322) | 2014 年 8 月 12 日  |
| 10.00.5867.00    | （按需更新包） |                         | [2888996](https://support.microsoft.com/zh-cn/help/2888996)、[2877204](https://support.microsoft.com/zh-cn/help/2877204)、[2920987](https://support.microsoft.com/zh-cn/help/2920987) |                     |
| 10.00.5861.00    | SP3            | CU17                    | [2958696](https://support.microsoft.com/zh-cn/help/2958696)  | 2014 年 5 月 19 日  |
| 10.00.5852.00    | SP3            | CU16                    | [2936421](https://support.microsoft.com/zh-cn/help/2936421)  | 2014 年 3 月 17 日  |
| 10.00.5850.00    | SP3            | CU15                    | [2923520](https://support.microsoft.com/zh-cn/help/2923520)  | 2014 年 1 月 20 日  |
| 10.00.5848.00    | SP3            | CU14                    | [2893410](https://support.microsoft.com/zh-cn/help/2893410)  | 2013 年 11 月 18 日 |
| 10.00.5846.00    | SP3            | CU13                    | [2880350](https://support.microsoft.com/zh-cn/help/2880350)  | 2013 年 9 月 16 日  |
| 10.00.5844.00    | SP3            | CU12                    | [2863205](https://support.microsoft.com/zh-cn/help/2863205)  | 2013 年 7 月 15 日  |
| 10.00.5840.00    | SP3            | CU11                    | [2834048](https://support.microsoft.com/zh-cn/help/2834048)  | 2013 年 5 月 20 日  |
| 10.00.5835.00    | SP3            | CU10                    | [2814783](https://support.microsoft.com/zh-cn/help/2814783)  | 2013 年 3 月 18 日  |
| 10.00.5829.00    | SP3            | CU9                     | [2799883](https://support.microsoft.com/zh-cn/help/2799883)  | 2013 年 1 月 21 日  |
| 10.00.5828.00    | SP3            | CU8                     | [2771833](https://support.microsoft.com/zh-cn/help/2771833)  | 2012 年 11 月 19 日 |
| 10.00.5826.00    | SP3            | MS12-070： QFE 安全更新 | [2716435](https://support.microsoft.com/zh-cn/help/2716435)  | 2012 年 10 月 9 日  |
| 10.00.5794.00    | SP3            | CU7                     | [2738350](https://support.microsoft.com/zh-cn/help/2738350)  | 2012 年 9 月 17 日  |
| 10.00.5788.00    | SP3            | CU6                     | [2715953](https://support.microsoft.com/zh-cn/help/2715953)  | 2012 年 7 月 16 日  |
| 10.00.5785.00    | SP3            | CU5                     | [2696626](https://support.microsoft.com/zh-cn/help/2696626)  | 2012 年 5 月 21 日  |
| 10.00.5775.00    | SP3            | CU4                     | [2673383](https://support.microsoft.com/zh-cn/help/2673383)  | 2012 年 3 月 19 日  |
| 10.00.5770.00    | SP3            | CU3                     | [2648098](https://support.microsoft.com/zh-cn/help/2648098)  | 2012 年 1 月 16 日  |
| 10.00.5768.00    | SP3            | CU2                     | [2633143](https://support.microsoft.com/zh-cn/help/2633143)  | 2011 年 11 月 21 日 |
| 10.00.5766.00    | SP3            | CU1                     | [2617146](https://support.microsoft.com/zh-cn/help/2617146)  | 2011 年 10 月 17 日 |
| 10.00.5538.00    | SP3            | MS15-058： GDR 安全更新 | [3045305](https://support.microsoft.com/zh-cn/help/3045305)  | 2015 年 7 月 14 日  |
| 10.00.5520.00    | SP3            | MS14-044： GDR 安全更新 | [2977321](https://support.microsoft.com/zh-cn/help/2977321)  | 2014 年 8 月 12 日  |
| 10.00.5512.00    | SP3            | MS12-070： GDR 安全更新 | [2716436](https://support.microsoft.com/zh-cn/help/2716436)  | 2012 年 10 月 9 日  |
| 10.00.5500.00    | SP3            | RTW/PCU 3               | [2546951](https://support.microsoft.com/zh-cn/help/2546951)  | 2011 年 10 月 6 日  |
| 10.00.4371.00    | SP2            | MS12-070： QFE 安全更新 | [2716433](https://support.microsoft.com/zh-cn/help/2716433)  | 2012 年 10 月 9 日  |
| 10.00.4333.00    | SP2            | CU11                    | [2715951](https://support.microsoft.com/zh-cn/help/2715951)  | 2012 年 7 月 16 日  |
| 10.00.4332.00    | SP2            | CU10                    | [2696625](https://support.microsoft.com/zh-cn/help/2696625)  | 2012 年 5 月 21 日  |
| 10.00.4330.00    | SP2            | CU9                     | [2673382](https://support.microsoft.com/zh-cn/help/2673382)  | 2012 年 3 月 19 日  |
| 10.00.4326.00    | SP2            | CU8                     | [2648096](https://support.microsoft.com/zh-cn/help/2648096)  | 2012 年 1 月 16 日  |
| 10.00.4323.00    | SP2            | CU7                     | [2617148](https://support.microsoft.com/zh-cn/help/2617148)  | 2011 年 11 月 21 日 |
| 10.00.4321.00    | SP2            | CU6                     | [2582285](https://support.microsoft.com/zh-cn/help/2582285)  | 2011 年 9 月 19 日  |
| 10.00.4316.00    | SP2            | CU5                     | [2555408](https://support.microsoft.com/zh-cn/help/2555408)  | 2011 年 7 月 18 日  |
| 10.00.4311.00    | SP2            | MS11-049： QFE 安全更新 | [2494094](https://support.microsoft.com/zh-cn/help/2494094)  | 2011 年 6 月 14 日  |
| 10.00.4285.00    | SP2            | CU4                     | [2527180](https://support.microsoft.com/zh-cn/help/2527180)  | 2011 年 5 月 16 日  |
| 10.00.4279.00    | SP2            | CU3                     | [2498535](https://support.microsoft.com/zh-cn/help/2498535)  | 2011 年 3 月 17 日  |
| 10.00.4272.00    | SP2            | CU2                     | [2467239](https://support.microsoft.com/zh-cn/help/2467239)  | 2011 年 1 月 17 日  |
| 10.00.4266.00    | SP2            | CU1                     | [2289254](https://support.microsoft.com/zh-cn/help/2289254)  | 2010 年 11 月 15 日 |
| 10.00.4067.00    | SP2            | MS12-070： GDR 安全更新 | [2716434](https://support.microsoft.com/zh-cn/help/2716434)  | 2012 年 10 月 9 日  |
| 10.00.4064.00    | SP2            | MS11-049： GDR 安全更新 | [2494089](https://support.microsoft.com/zh-cn/help/2494089)  | 2011 年 6 月 14 日  |
| 10.00.4000.00    | SP2            | RTW/PCU 2               | [2285068](https://support.microsoft.com/zh-cn/help/2285068)  | 2010 年 9 月 29 日  |
| 10.00.2850.0     | SP1            | CU16                    | [2582282](https://support.microsoft.com/zh-cn/help/2582282)  | 2011 年 9 月 19 日  |
| 10.00.2847.0     | SP1            | CU15                    | [2555406](https://support.microsoft.com/zh-cn/help/2555406)  | 2011 年 7 月 18 日  |
| 10.00.2841.0     | SP1            | MS11-049： QFE 安全更新 | [2494100](https://support.microsoft.com/zh-cn/help/2494100)  | 2011 年 6 月 14 日  |
| 10.00.2821.00    | SP1            | CU14                    | [2527187](https://support.microsoft.com/zh-cn/help/2527187)  | 2011 年 5 月 16 日  |
| 10.00.2816.00    | SP1            | CU13                    | [2497673](https://support.microsoft.com/zh-cn/help/2497673)  | 2011 年 3 月 17 日  |
| 10.00.2808.00    | SP1            | CU12                    | [2467236](https://support.microsoft.com/zh-cn/help/2467236)  | 2011 年 1 月 17 日  |
| 10.00.2804.00    | SP1            | CU11                    | [2413738](https://support.microsoft.com/zh-cn/help/2413738)  | 2010 年 11 月 15 日 |
| 10.00.2799.00    | SP1            | CU10                    | [2279604](https://support.microsoft.com/zh-cn/help/2279604)  | 2010 年 9 月 20 日  |
| 10.00.2789.00    | SP1            | CU9                     | [2083921](https://support.microsoft.com/zh-cn/help/2083921)  | 2010 年 7 月 19 日  |
| 10.00.2775.00    | SP1            | CU8                     | [981702](https://support.microsoft.com/zh-cn/help/981702)    | 2010 年 5 月 17 日  |
| 10.00.2766.00    | SP1            | CU7                     | [979065](https://support.microsoft.com/zh-cn/help/979065)    | 2010 年 3 月 26 日  |
| 10.00.2757.00    | SP1            | CU6                     | [977443](https://support.microsoft.com/zh-cn/help/977443)    | 2010 年 1 月 18 日  |
| 10.00.2746.00    | SP1            | CU5                     | [975977](https://support.microsoft.com/zh-cn/help/975977)    | 2009 年 11 月 16 日 |
| 10.00.2734.00    | SP1            | CU4                     | [973602](https://support.microsoft.com/zh-cn/help/973602)    | 2009 年 9 月 21 日  |
| 10.00.2723.00    | SP1            | CU3                     | [971491](https://support.microsoft.com/zh-cn/help/971491)    | 2009 年 7 月 20 日  |
| 10.00.2714.00    | SP1            | CU2                     | [970315](https://support.microsoft.com/zh-cn/help/970315)    | 2009 年 5 月 18 日  |
| 10.00.2710.00    | SP1            | CU1                     | [969099](https://support.microsoft.com/zh-cn/help/969099)    | 2009 年 4 月 16 日  |
| 10.00.2573.00    | SP1            | MS11-049： GDR 安全更新 | [2494096](https://support.microsoft.com/zh-cn/help/2494096)  | 2011 年 6 月 14 日  |
| 10.00.2531.00    | SP1            | RTW/PCU 1               |                                                              | 2009 年 4 月        |
| 10.00.1835.00    | RTM            | CU10                    | [979064](https://support.microsoft.com/zh-cn/help/979064)    | 2010 年 3 月 15 日  |
| 10.00.1828.00    | RTM            | CU9                     | [977444](https://support.microsoft.com/zh-cn/help/977444)    | 2010 年 1 月 18 日  |
| 10.00.1823.00    | RTM            | CU8                     | [975976](https://support.microsoft.com/zh-cn/help/975976)    | 2009 年 11 月 16 日 |
| 10.00.1818.00    | RTM            | CU7                     | [973601](https://support.microsoft.com/zh-cn/help/973601)    | 2009 年 9 月 21 日  |
| 10.00.1812.00    | RTM            | CU6                     | [971490](https://support.microsoft.com/zh-cn/help/971490)    | 2009 年 7 月 20 日  |
| 10.00.1806.00    | RTM            | CU5                     | [969531](https://support.microsoft.com/zh-cn/help/969531)    | 2009 年 5 月 18 日  |
| 10.00.1798.00    | RTM            | CU4                     | [963036](https://support.microsoft.com/zh-cn/help/963036)    | 2009 年 3 月 16 日  |
| 10.00.1787.00    | RTM            | CU3                     | [960484](https://support.microsoft.com/zh-cn/help/960484)    | 2009 年 1 月 19 日  |
| 10.00.1779.00    | RTM            | CU2                     | [958186](https://support.microsoft.com/zh-cn/help/958186)    | 2008 年 11 月 19 日 |
| 10.00.1763.00    | RTM            | CU1                     | [956717](https://support.microsoft.com/zh-cn/help/956717)    | 2008 年 9 月 22 日  |
| 10.00.1600.22    | RTM            |                         |                                                              | 2008 年 8 月 6 日   |



​	综上所述，根据微软官方的推荐，决定下载SQL Server 2019的Express版本，一是因为Express版本较为轻量，放在主机上做实验比较方便；二是因为SQL Server的2008版本已经不在官网提供下载路径，2019的社区环境较好，值得下载。



### 1.3 下载软件安装包

​	首先在谷歌搜索SQL Server，进入微软的官方网站。

![2020-09-08-15.45.33.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-15.45.33.png)

<center>图4</center>

​	进入网站以后可以看到相关的下载界面。可以看到SQL Server 2019 on-premises选项下的Download free trial。这里选择的都是云服务器上的SQL Server版本。

![2020-09-08-00.50.12.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.50.12.png)

<center>图5</center>

​	下拉页面，可以看到个人用户的版本，选择免费版本。

![2020-09-08-00.50.39.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.50.39.png)

<center>图6</center>

​		这里免费版本又有两种版本，那么如何在Express和Developer之间进行选择呢？在微软官网上，我找到了具体的比较参数表格。

| Features                                                     | SQL Server 2019 Enterprise                                   | SQL Server 2019 Standard                                     | SQL Server 2019 Express                                      | SQL Server 2019 Developer                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Scale**                                                    |                                                              |                                                              |                                                              |                                                              |
| Maximum number of cores                                      | Unlimited                                                    | 24 cores                                                     | 4 cores                                                      | Unlimited                                                    |
| **Memory:** Maximum buffer pool size per instance            | Operating system max                                         | 128 GB                                                       | 1410 MB                                                      | Operating system max                                         |
| **Memory:** Maximum Columnstore segment cache per instance   | Operating system max                                         | 32 GB                                                        | 352 MB                                                       | Operating system max                                         |
| **Memory:** Maximum memory-optimized data per database       | Operating system max                                         | 32 GB                                                        | 352 MB                                                       | Operating system max                                         |
| Maximum database size                                        | 524 PB                                                       | 524 PB                                                       | 10 GB                                                        | 524 PB                                                       |
| Production use rights                                        | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Unlimited virtualization, a software assurance benefit       | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Programmability**                                          |                                                              |                                                              |                                                              |                                                              |
| **Programmability and developer tools:** T-SQL, SQL CLR, Service Broker, JSON, XML, graph data support | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **OLTP performance**                                         |                                                              |                                                              |                                                              |                                                              |
| **Advanced OLTP:** in-memory OLTP, operational analytics [3] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Manageability:** Management Studio, policy-based management | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Basic high availability:** two-node single database failover, non-readable secondary | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Advanced high availability:** Always On Availability Groups, multi-database failover, readable secondaries | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Security**                                                 |                                                              |                                                              |                                                              |                                                              |
| **Advanced security:** Always Encrypted Row-level security, data masking | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Compliance reporting with SQL Server audit                   | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Transparent data encryption                                  | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Data integration**                                         |                                                              |                                                              |                                                              |                                                              |
| **Advanced data integration:** fuzzy grouping and look ups   | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Data warehousing**                                         |                                                              |                                                              |                                                              |                                                              |
| **Data marts and data warehousing:** partitioning, data compression, change data capture, database snapshot | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| In-memory columnstore [3]                                    | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Adaptive Query Processing [6]                                | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| PolyBase [4], [5]                                            | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Enterprise data management:** Master Data Services, Data Quality Services [5] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Business intelligence**                                    |                                                              |                                                              |                                                              |                                                              |
| Maximum memory utilized per instance of Analysis Services [5] | Operating system max                                         | Tabular: 16 GBMOLAP: 64 GB                                   | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | Operating system max                                         |
| Maximum memory utilized per instance of Reporting Services [5] | Operating system max                                         | 64 GB                                                        | Express with Advanced Services: 4 GB                         | Operating system max                                         |
| Basic reporting and analytics [5]                            | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Basic data integration:** SQL Server Integration Services, built-in connectors | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Basic corporate business intelligence:** basic multi-dimensional models, basic tabular model, in-memory storage mode [5] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Mobile reports and KPIs [5]                                  | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Advanced corporate business intelligence:** advanced multi-dimensional models, advanced tabular model, DirectQuery storage mode, advanced data mining [5] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Access to Power BI Report Server, a software assurance benefit | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Advanced analytics**                                       |                                                              |                                                              |                                                              |                                                              |
| **Basic Machine Learning integration:** connectivity to open source Python and R, limited parallelism [5] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Advanced Machine Learning integration:** full parallelism of R and Python analytics and the ability to run on GPUs [5] | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| Machine Learning for Hadoop/Spark and Machine Learning for Linux, a software assurance benefit | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |
| **Hybrid cloud**                                             |                                                              |                                                              |                                                              |                                                              |
| Stretch Database [5]                                         | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tl6o?ver=b724&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) | ![img](https://img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/RE4tpGe?ver=d0e6&q=90&m=6&h=15&w=15&b=%23FFFFFFFF&l=f&o=t&aim=true) |



​	我选择了developer版本的SQL Server，这个在之后的文章中会讲到，但是在官网下载过程中，除非是通过制作镜像来完成安装，否则是不需要选择大版本中的具体版本类型的。

​	紧接着进行操作系统的选择，在Docker、Linux和Windows之间选择Windows版本。

![2020-09-08-00.50.53.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.50.53.png)

<center>图7</center>

​	

​	在选择Windows系统后，微软依然十分贴心的提供了Azure云服务的SQL Server下载版本。我们直接选择Install on Windows选项。

![2020-09-08-00.51.09.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.51.09.png)

<center>图8</center>

​	

​	进入下载界面后，就有大版本的选择选项了，这里按照之前已经陈述的版本选择原则去获取下载链接。

![2020-09-08-00.51.47.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.51.47.png)

<center>图9</center>



​	选取exe版本：

![2020-09-08-00.52.12.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.52.12.png)

<center>图10</center>



​	确认版本信息：

![2020-09-08-00.52.43.png](http://panzy25.ticp.io:4000/images/2020/09/08/2020-09-08-00.52.43.png)

<center>图11</center>



​	完成下载链接后，我们使用管理员权限打开安装程序：

![1.png](http://panzy25.ticp.io:4000/images/2020/09/08/1.png)

<center>图12</center>



​	接下来就需要查阅软件安装操作手册进行安装。



## 2. 查询以及下载软件安装操作手册

### 2.1 查询软件安装手册

​	使用谷歌搜索引擎搜索`SQL Server2019安装手册`.

![6ae00fba0a9da0431aaf58da3816f5ac.png](http://panzy25.ticp.io:4000/images/2020/09/08/6ae00fba0a9da0431aaf58da3816f5ac.png)

<center>图13</center>



​	选择微软官方的查询链接：[SQL Server 安装指南](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server?view=sql-server-ver15)，即可获得相关的安装指南。

![f6c08ac94eec96905a16090b6f62bc96.png](http://panzy25.ticp.io:4000/images/2020/09/08/f6c08ac94eec96905a16090b6f62bc96.png)

<center>图14</center>



### 2.2 SQL Server安装手册

#### 2.2.1 概述

**适用于：**![是](https://docs.microsoft.com/zh-cn/sql/includes/media/yes-icon.png?view=sql-server-ver15)SQL Server（所有支持的版本）-仅限 Windows

本文是内容索引，提供关于在 Windows 上安装 SQL Server 的指南。

有关其他部署方案，请参阅：

- [Linux](https://docs.microsoft.com/zh-cn/sql/linux/sql-server-linux-setup?view=sql-server-ver15)
- [Docker 容器](https://docs.microsoft.com/zh-cn/sql/linux/sql-server-linux-configure-docker?view=sql-server-ver15)
- [Kubernetes - 大数据群集](https://docs.microsoft.com/zh-cn/sql/big-data-cluster/deploy-get-started?view=sql-server-ver15)

从 SQL Server 2016 (13.x) 开始，SQL Server 仅可用作 64 位应用程序。 以下是有关如何获取 SQL Server 以及如何安装 SQL Server 的重要详细信息。

##### 入门

- **版本和功能**：查看不同版本 SQL Server 支持的功能，以确定最适合你业务需求的功能。
  - [SQL Server 2019 (15.x)](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-version-15?view=sql-server-ver15)：
  - [SQL Server 2017 (14.x)](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2017?view=sql-server-ver15)：
  - [SQL Server 2016 (13.x)](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2016?view=sql-server-ver15)：
  - [SQL Server 2014 (12.x)](https://docs.microsoft.com/zh-cn/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014)
- **要求**：查看 [SQL Server 2016 和 2017](https://docs.microsoft.com/zh-cn/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-ver15)、[SQL Server 2019](https://docs.microsoft.com/zh-cn/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-ver15) 或 [Linux 上的 SQL Server](https://docs.microsoft.com/zh-cn/sql/linux/sql-server-linux-setup?view=sql-server-ver15) 的硬件和软件安装要求，以及系统配置检查和[规划 SQL Server 安装中](https://docs.microsoft.com/zh-cn/sql/sql-server/install/planning-a-sql-server-installation?view=sql-server-ver15)的安全注意事项
- **示例数据库和示例代码**：
  - 默认情况下，它们不作为 SQL Server 安装程序的一部分安装，但可以找到它们
  - 要为非 Express 版本的 SQL Server 安装它们，请参阅[示例存储库](https://docs.microsoft.com/zh-cn/sql/samples/sql-samples-where-are?view=sql-server-ver15)

##### 安装媒体

SQL Server 的下载位置由版本决定：

- “SQL Server Enterprise、Standard 和 Express Edition”已获授权，可供生产之用。 对于企业版和标准版，请联系软件供应商获取安装媒体。 可以在 [Microsoft 许可页面](https://www.microsoft.com/licensing/product-licensing/sql-server)上找到采购信息和 Microsoft 合作伙伴目录。
- [免费版本 - 最新](https://www.microsoft.com/sql-server/sql-server-downloads)
- [免费版本 - 其他](https://www.microsoft.com/evalcenter/evaluate-sql-server)

可在此处找到其他 SQL Server 组件：

- [所有累积更新](https://sqlserverbuilds.blogspot.com/)
- [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)。
- [SQL Server Management Studio](https://aka.ms/ssmsfullsetup)
- [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)

##### 注意事项

- 如果通过远程桌面连接 RDC 客户端上本地资源中的介质来启动安装程序，安装将会失败。 若要执行远程安装，介质必须处于网络共享状态，或是物理计算机或虚拟机的本地介质。 SQL Server 安装介质要么处于网络共享状态，要么是映射的驱动器、本地驱动器，或者是虚拟机的 ISO。
- SQL Server 安装程序安装该产品所需的以下软件组件：
  - SQL Server Native Client
  - SQL Server 安装程序支持文件

##### SQL Server 安装

| 项目                                                         | 说明                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [安装向导](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup?view=sql-server-ver15) | 使用从 setup.exe 安装媒体启动的安装向导 GUI 安装 SQL Server。 |
| [命令提示符](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-2016-from-the-command-prompt?view=sql-server-ver15) | 用于从命令提示符运行 SQL Server 安装的示例语法和安装参数。   |
| [Server Core](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-ver15) | 在 Windows Server Core 上安装 SQL Server。                   |
| [系统配置检查器的检查参数](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/check-parameters-for-the-system-configuration-checker?view=sql-server-ver15) | 讨论系统配置检查器 (SCC) 的功能。                            |
| [配置文件](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-2016-using-a-configuration-file?view=sql-server-ver15) | 用于通过配置文件运行安装程序的示例语法和安装参数。           |
| [SysPrep](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-using-sysprep?view=sql-server-ver15) | 用于通过 SysPrep 运行安装程序的示例语法和安装参数。          |
| [将功能添加到实例](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup?view=sql-server-ver15) | 更新 SQL Server 现有实例的组件。                             |
| [SQL Server 故障转移群集安装](https://docs.microsoft.com/zh-cn/sql/sql-server/failover-clusters/install/sql-server-failover-cluster-installation?view=sql-server-ver15) | 安装 SQL Server 故障转移群集实例。                           |
| [修复失败的 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/repair-a-failed-sql-server-installation?view=sql-server-ver15) | 修复损坏的 SQL Server 安装。                                 |
| [使用 SQL Server 重命名计算机](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server?view=sql-server-ver15) | 在重命名托管 SQL Server 独立实例的计算机的主机名之后，更新存储在 sys.servers 中的系统元数据。 |
| [安装 SQL Server 服务更新](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-servicing-updates?view=sql-server-ver15) | 安装 SQL Server 的更新。                                     |
| [安装程序日志文件](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files?view=sql-server-ver15) | 查看和读取 SQL Server 安装程序日志文件中的错误。             |
| [验证安装](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/validate-a-sql-server-installation?view=sql-server-ver15) | 查看 SQL 发现报告的用法，以便确认 SQL Server 的版本以及在计算机上安装的 SQL Server 功能。 |

##### 单个组件安装

| 项目                                                         | 说明                                           |
| :----------------------------------------------------------- | :--------------------------------------------- |
| [SQL Server 数据库引擎](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-database-engine?view=sql-server-ver15) | 安装和配置 SQL Server 数据库引擎。             |
| [SQL Server 复制](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-replication?view=sql-server-ver15) | 安装和配置 SQL Server 复制。                   |
| [Distributed Replay](https://docs.microsoft.com/zh-cn/sql/tools/distributed-replay/install-distributed-replay-overview?view=sql-server-ver15) | 列出了有关安装 Distributed Replay 功能的文章。 |
| [带有 SSMS 的 SQL Server 管理工具](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381) | 安装和配置 SQL Server 管理工具。               |
| [SQL Server PowerShell](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-powershell?view=sql-server-ver15) | 安装 SQL Server PowerShell 组件的注意事项。    |

##### SQL Server 配置

| 项目                                                         | 说明                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [配置 Windows 防火墙 (SQL Server)](https://docs.microsoft.com/zh-cn/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access?view=sql-server-ver15) | 概述防火墙配置以及如何配置 Windows 防火墙以允许访问 SQL Server。 |
| [配置 Windows 防火墙 (SSAS)](https://docs.microsoft.com/zh-cn/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access) | 配置端口和防火墙设置，以允许访问 Analysis Services 或用于 SharePoint 的 Power Pivot。 |
| [配置多宿主计算机](https://docs.microsoft.com/zh-cn/sql/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access?view=sql-server-ver15) | 配置 SQL Server 和具有高级安全性的 Windows 防火墙，以便在多宿主环境中与 SQL Server 实例建立网络连接。 |



#### 2.2.2 安装向导帮助

**适用于：** ![是](https://docs.microsoft.com/zh-cn/sql/includes/media/yes-icon.png?view=sql-server-ver15)SQL Server（所有支持的版本）

本文介绍 SQL Server 安装向导中的一些配置页。



##### “实例配置”页

使用 **安装向导的** “实例配置” SQL Server 页面可指定是创建 SQL Server的默认实例还是其命名实例。 如果 SQL Server 实例尚未安装，系统就会创建默认实例，除非你指定命名实例。

每个 SQL Server 实例都由一组具有排列规则及其他选项特定设置的非重复的服务组成。 目录结构、注册表结构和服务名称全都反映在 SQL Server 安装过程中创建的实例名称和具体实例 ID。

实例是默认实例或命名实例。 默认实例名为 MSSQLSERVER。 使用默认名称，客户端无需指定实例名称，即可进行连接。 命名实例在安装过程中由用户决定。 您可以将 SQL Server 作为命名实例安装，无需先安装默认实例。 一次只能有一个 SQL Server 安装是默认实例，无论版本如何。

 备注

使用 SQL Server SysPrep，您可以在 **“实例配置”** 页上完成已准备实例时指定实例名称。 如果计算机上现无 SQL Server 默认实例，可以将要完成的已准备实例配置为默认实例。



###### 多个实例

SQL Server 支持在单个服务器或处理器上存在多个 SQL Server 实例，但只能有一个实例为默认实例。 所有其他实例必须为命名实例。 一台计算机可同时运行多个 SQL Server 实例，每个实例都独立于其他实例运行。

有关详细信息，请参阅 [SQL Server 最大容量规范](https://docs.microsoft.com/zh-cn/sql/sql-server/maximum-capacity-specifications-for-sql-server?view=sql-server-ver15)。



###### 选项

**仅故障转移群集实例**：指定 SQL Server 故障转移群集网络名称。 此名称可用来在网络上标识故障转移群集实例。

**决定使用默认实例还是命名实例**：决定是安装 SQL Server 默认实例还是命名实例时，请注意以下几点：

- 如果计划在数据库服务器上安装单个 SQL Server 实例，则该实例应为默认实例。
- 如果您打算在同一台计算机上安装多个实例，请使用命名实例。 一台服务器只能承载一个默认实例。
- 任何安装 SQL Server Express 的应用程序都应将其作为命名实例安装。 如果同一台计算机中安装有多个应用程序，这种做法可以最大限度地减少冲突。

**默认实例**：选择该选项可安装 SQL Server 的默认实例。 一台计算机只能托管一个默认实例；所有其他实例必须是命名实例。 但是，如果您已经安装了 SQL Server 的默认实例，则可以向同一台计算机添加 Analysis Services 的默认实例。

**命名实例**：选择该选项可创建新的命名实例。 命名 SQL Server 实例时，请注意以下几点：

- 实例名称不区分大小写。

- 实例名称不得以下划线 (*) 开头或结尾。*

- 实例名称不得包含“Default”一词或其他保留关键字。 如果在实例名称中使用了保留关键字，就会看到安装程序错误。 有关详细信息，请参阅[保留关键字 (Transact-SQL)](https://docs.microsoft.com/zh-cn/sql/t-sql/language-elements/reserved-keywords-transact-sql?view=sql-server-ver15)。

- 如果为实例名称指定 MSSQLSERVER，创建的是默认实例。

- Microsoft SQL Server 2016 Power Pivot for SharePoint 安装始终安装为“Power Pivot”的命名实例。 不得为此功能角色指定其他实例名称。

- 实例名限制为 16 个字符。

- 实例名中的第一个字符必须是字母。 可接受的字母由 Unicode 标准 2.0 定义。 这些字母包括拉丁字符 a-z、A-Z 和其他语言中的字母字符。

- 后续字符可以是 Unicode 标准 2.0 定义的字母、源于基本拉丁语或其他国家/地区书写符号的十进制数字、美元符号 ($) 或者下划线 (*)。*

- 禁止在实例名称中使用嵌入空格或其他特殊字符。 也禁止使用反斜杠 (\)、逗号 (,)、冒号 (:)、分号 (;)、单引号 (')、& 号 (&)、连字号 (-) 和 at 符号 (@)。

  只有在当前 Windows 代码页中有效的字符才能用在 SQL Server 实例名称中。 如果使用不受支持的 Unicode 字符，就会看到安装程序错误。

**检测到的实例和功能**：查看正在运行 SQL Server 安装程序的计算机中安装的 SQL Server 实例和组件的列表。

**实例 ID**：默认情况下，实例名称用作实例 ID。 此 ID 用于标识 SQL Server 实例的安装目录和注册表项。 对于默认实例和命名实例，行为是相同的。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认实例 ID，请在“实例 ID”字段中指定它。

 重要

如果使用 SQL Server SysPrep，“实例配置”**** 页上显示的实例 ID 是，在 SQL Server SysPrep 过程的准备映像步骤中指定的实例 ID。 无法在完成映像步骤中指定其他实例 ID。

 备注

不支持以下划线 (*) 开头或包含数字符号 (#) 或美元符号 ($) 的实例 ID。*

若要详细了解目录、文件位置和实例 ID 命名，请参阅 [SQL Server 默认实例和命名实例的文件位置](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-ver15)。

SQL Server 的给定实例的所有组件作为一个单元进行管理。 所有 SQL Server Service Pack 和升级都适用于 SQL Server 实例的每个组件。

共用同一实例名称的所有 SQL Server 组件都必须满足以下条件：

- 版本相同
- 版本类别相同
- 语言设置相同
- 聚集状态相同
- 操作系统相同

 备注

Reporting Services 不是群集感知应用程序。



##### “Analysis Services 配置 - 帐户预配”页

此页可用于设置服务器节点，并向需要不受限制地访问 Analysis Services 的用户或服务授予管理权限。 安装程序不会自动将本地 Windows 组 BUILTIN\Administrators 添加到要安装的实例的 Analysis Services 服务器管理员角色。 如果要将本地管理员组添加到服务器管理员角色，则必须显式指定该组。

若要安装 Power Pivot for SharePoint，请务必向负责在 SharePoint Server 2010 场中部署 Power Pivot 服务器的 SharePoint 场管理员或服务管理员授予管理权限。



###### 选项

**服务器模式**：服务器模式指定可部署到服务器的 Analysis Services 数据库的类型。 服务器模式是在你使用安装程序期间进行确定，之后便无法再修改。 每种模式都是互斥的；也就是说，需要两个 Analysis Services 实例，并为每个实例配置不同的模式，以同时支持典型联机分析处理 (OLAP) 和表格模型解决方案。

**指定管理员**：必须为 SQL Server 实例指定至少一个服务器管理员。 你指定的用户或组成为要安装的 Analysis Services 实例的服务器管理员角色成员。 此类成员必须拥有 Windows 域用户帐户，这些帐户与要在其上安装软件的计算机处于同一域中。

 备注

用户帐户控制 (UAC) 是一项 Windows 安全功能，它要求管理操作或应用程序必须先获得管理员专门批准，然后才能运行。 由于 UAC 默认处于启用状态，因此系统会提示你允许执行需要提升的权限的特定操作。 可以将 UAC 配置为更改默认行为，也可以为特定程序自定义 UAC。 若要详细了解 UAC 和 UAC 配置，请参阅[用户帐户控制分步指南](https://go.microsoft.com/fwlink/?linkid=196350)和[用户帐户控制 (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351)。



###### 另请参阅

- [配置服务帐户 (Analysis Services)](https://docs.microsoft.com/zh-cn/analysis-services/instances/configure-service-accounts-analysis-services)
- [配置 Windows 服务帐户和权限](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15)



##### “Analysis Services 配置 - 数据目录”页

下表中的默认目录是在 SQL Server 安装过程中可由用户配置的目录。 对这些文件的访问权限授予给本地管理员，以及在使用安装程序期间创建并预配的 SQLServerMSASUser$<instance> 安全组的成员。

###### UI 元素列表

| 说明             | 默认目录                                                     | 建议                                                         |
| :--------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **数据根目录**   | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Data\ | 确保通过限制权限对 \Program files\Microsoft SQL Server\ 文件夹进行保护。 在许多配置中，Analysis Services 性能取决于数据目录所在的存储区的性能。 请将此目录置于已附加到系统的性能最高存储中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。 |
| **日志文件目录** | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Log\ | 此目录用于 Analysis Services 日志文件，其中包括 FlightRecorder 日志。 如果要延长网络流量记录器持续时间，请确保该日志目录有足够的空间。 |
| **临时目录**     | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Temp\ | 请将临时目录置于高性能存储子系统中。                         |
| **备份目录**     | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Backup\ | 此目录用于 Analysis Services 默认备份文件。 对于 Power Pivot for SharePoint 安装，此目录也是 Power Pivot 系统服务缓存 Power Pivot 数据文件的位置。  请确保适当权限已设置以防数据丢失，并确保 Analysis Services 的用户组拥有足够的权限，可以对备份目录执行写入操作。 不支持对备份目录使用映射驱动器。 |



###### 注意事项

- 在部署到 SharePoint 场后，Analysis Services 实例将应用程序文件、数据文件和属性存储在内容数据库和服务应用程序数据库中。
- 向现有安装添加功能时，既不得更改以前安装的功能的位置，也不得为新功能指定位置。
- 可能需要安装扫描软件（如防病毒应用程序和反间谍应用程序）以排除 SQL Server 文件夹和文件类型。 有关详细信息，请参阅以下支持文章：[运行 SQL Server 的计算机上的防病毒软件](https://support.microsoft.com/kb/309422)。
- 如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 不要将此对话框中的目录分与其他 SQL Server 实例中的目录。 还请在 SQL Server 实例中安装 数据库引擎 和 Analysis Services 组件，以分隔目录。
- 在下列情况下，无法安装程序文件和数据文件：
  - 在可移动磁盘驱动器上
  - 在使用压缩的文件系统上
  - 在系统文件所在的目录上



###### 另请参阅

若要详细了解目录、文件位置和实例 ID 命名，请参阅 [SQL Server 默认实例和命名实例的文件位置](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-ver15)。



##### “Analysis Services 配置 - 数据目录”页

下表中的默认目录是在 SQL Server 安装过程中可由用户配置的目录。 对这些文件的访问权限授予给本地管理员，以及在使用安装程序期间创建并预配的 SQLServerMSASUser$<instance> 安全组的成员。

###### UI 元素列表

| 说明             | 默认目录                                                     | 建议                                                         |
| :--------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **数据根目录**   | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Data | 确保通过限制权限对 \Program files\Microsoft SQL Server\ 文件夹进行保护。 在许多配置中，Analysis Services 性能取决于数据目录所在的存储区的性能。 请将此目录置于已附加到系统的性能最高存储中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。 |
| **日志文件目录** | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Log | 此目录用于 Analysis Services 日志文件，其中包括 FlightRecorder 日志。 如果延长外部测试版记录器持续时间，请确保日志目录有足够空间。 |
| **临时目录**     | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Temp | 请将临时目录置于高性能存储子系统中。                         |
| **备份目录**     | <Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.<InstanceID>\OLAP\Backup | 此目录用于 Analysis Services 默认备份文件。 对于 Power Pivot for SharePoint 安装，这也是 Power Pivot 系统服务缓存 Power Pivot 数据文件的位置。  确保设置合适的权限以防止数据丢失，并确保 Analysis Services 服务的用户组具有写入备份目录的足够权限。 不支持对备份目录使用映射驱动器。 |



###### 注意事项

- 在部署到 SharePoint 场后，Analysis Services 实例将应用程序文件、数据文件和属性存储在内容数据库和服务应用程序数据库中。
- 向现有安装添加功能时，既不得更改以前安装的功能的位置，也不得为新功能指定位置。
- 可能需要安装扫描软件（如防病毒应用程序和反间谍应用程序）以排除 SQL Server 文件夹和文件类型。 有关详细信息，请参阅[运行 SQL Server 的计算机上的防病毒软件](https://support.microsoft.com/kb/309422)。
- 如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 不要将此对话框中的目录分与其他 SQL Server 实例中的目录。 还请在 SQL Server 实例中安装 数据库引擎 和 Analysis Services 组件，以分隔目录。
- 在下列情况下，无法安装程序文件和数据文件：
  - 在可移动磁盘驱动器上
  - 在使用压缩的文件系统上
  - 在系统文件所在的目录上

###### 另请参阅

- 若要详细了解目录、文件位置和实例 ID 命名，请参阅 [SQL Server 默认实例和命名实例的文件位置](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-ver15)
- [文件服务器上的共享权限和 NTFS 权限](https://docs.microsoft.com/zh-cn/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)



##### “数据库引擎配置 - 服务器配置”页

此页可用于设置 SQL Server 安全模式，并将 Windows 用户或组添加为 SQL Server 数据库引擎管理员。



###### 关于运行 SQL Server 2019 (15.x) 的注意事项

在旧版 SQL Server中，BUILTIN\Administrators 组被预配为 数据库引擎中的登录名，本地 Administrators 组的成员可以使用自己的管理员凭据登录。 不过，使用提升的权限并不是最佳做法。

在 SQL Server 2019 (15.x) 中，BUILTIN\Administrators 组未被预配为登录名。 请务必为每个管理用户都创建 SQL Server 登录名，并在安装 SQL Server 2019 (15.x) 新实例的过程中将相应登录名添加到 sysadmin**** 固定服务器角色中。 对运行 SQL Server 代理作业（包括复制代理作业）的 Windows 帐户执行相同操作。



###### 选项

**安全模式**：为安装选择“Windows 身份验证”或“混合模式身份验证”。

**Windows 主体预配**：在旧版 SQL Server 中，Windows BUILTIN\Administrators 本地组被添加到 SQL Server sysadmin 服务器角色中，有效地向 Windows 管理员授予对 SQL Server 实例的访问权限。 在 SQL Server 2019 (15.x) 中，BUILTIN\Administrators 组未在 sysadmin 服务器角色中进行预配。 而是改为由您在安装过程中为新安装显式设置 SQL Server 管理员。

 重要

您在安装过程中必须为新安装显式设置 SQL Server 管理员。 除非你完成这一步，否则安装程序不会允许你继续操作。

**指定 SQL Server 管理员**：必须为 SQL Server 实例指定至少一个 Windows 主体。 若要添加正在运行 SQL Server 安装程序的帐户，请选择“添加当前用户”按钮。 若要在系统管理员列表中添加或删除帐户，请先选择“添加”**** 或“删除”****，再编辑对 SQL Server 实例拥有管理员权限的用户、组或计算机列表。

编辑完列表后，选择“确定”，然后验证此配置对话框中的管理员列表。 如果列表是完整的，请单击“下一步”。

如果选择“混合模式身份验证”，必须为内置 SQL Server 系统管理员 (sa) 帐户提供登录凭据。

 重要

不要使用空密码。 请使用强密码。

**Windows 身份验证模式**：当用户通过 Windows 用户帐户连接时，SQL Server 使用操作系统中的 Windows 主体令牌来验证帐户名和密码。 Windows 身份验证是默认身份验证模式，比混合模式身份验证安全得多。 Windows 身份验证使用 Kerberos 安全协议，在验证强密码复杂性方面强制执行密码策略，并支持帐户锁定和密码到期。

 重要

请尽可能使用 Windows 身份验证。

 重要

不要使用空密码。 请使用强密码。 切勿设置空白或弱 sa 密码。

**混合模式(Windows 身份验证或 SQL Server 身份验证)** ：允许用户使用 Windows 身份验证或 SQL Server 身份验证进行连接。 通过 Windows 用户帐户进行连接的用户可以使用经过 Windows 验证的信任连接。

如果必须选择混合模式身份验证，且需要使用 SQL 登录名来适应旧版应用程序，必须为所有 SQL Server 帐户设置强密码。

 备注

提供 SQL Server 身份验证只是为了实现后向兼容性。 请尽可能使用 Windows 身份验证。

**输入密码**：输入并确认系统管理员 (sa) 登录名。 密码是抵御入侵者的第一道防线，因此设置强密码对于系统安全是绝对必要的。 切勿设置空白或弱 sa 密码。

 备注

SQL Server 密码可包含 1 到 128 个字符，包括字母、符号和数字的任意组合。 如果选择混合模式身份验证，必须先输入强 sa**** 密码，然后才能继续转到安装向导的下一页。



###### 强密码指南

强密码不易被人猜出，也不易被计算机程序破解。 强密码不得使用禁止的条件或字词，具体包括：

- 空条件或 NULL 条件
- “Password”
- “Admin”
- “Administrator”
- “sa”
- “sysadmin”

强密码不得是下列与安装计算机相关联的字词：

- 当前登录计算机的用户的用户名
- 计算机名称

强密码的长度必须多于 8 个字符，并且强密码至少要满足下列四个条件中的三个：

- 它必须包含大写字母。
- 它必须包含小写字母。
- 必须包含数字。
- 必须包含非字母数字字符；例如 #、% 或 ^。

你在此页上输入的密码必须符合强密码策略要求。 如果有任何使用 SQL Server 身份验证的自动化过程，请确保密码符合强密码策略要求。



###### 另请参阅

若要详细了解如何选择 Windows 身份验证与 SQL Server 身份验证，请参阅[选择身份验证模式](https://docs.microsoft.com/zh-cn/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver15)。

若要详细了解如何选择用于运行 SQL Server 数据库引擎的帐户，请参阅[配置 Windows 服务帐户和权限](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15)。



##### “数据库引擎配置 - 数据目录”页

此页面可用于指定 SQL Server 数据库引擎 程序和数据文件的安装位置。 根据安装类型，支持的存储可能包括本地磁盘、共享存储或 SMB 文件服务器。

若要将 SMB 文件共享指定为目录，您必须手动键入支持的 UNC 路径。 不支持转到 SMB 文件共享。 下面的示例展示了受支持的 SMB 文件共享 UNC 路径格式：

```
\\<ServerName>\<ShareName>\...
```

###### SQL Server 独立实例

对于 SQL Server 独立实例，下表列出了受支持的存储类型，以及你可以在 SQL Server 安装过程中配置的默认目录：

###### UI 元素列表

| 说明                   | 受支持的存储类型                    | 默认目录                                                     | 建议                                                         |
| :--------------------- | :---------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **数据根目录**         | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\                 | SQL Server 安装程序为 SQL Server 目录配置访问控制列表 (ACL)，并在配置过程中中断继承。 |
| **用户数据库目录**     | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data | 用户数据目录的最佳实践取决于工作量和性能要求。               |
| **用户数据库日志目录** | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data | 确保日志目录有足够的空间。                                   |
| **备份目录**           | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Backup | 设置合适的权限以防止数据丢失，并确保 SQL Server 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射驱动器。 |

*尽管共享磁盘受支持，但不建议将共享磁盘用于 SQL Server 独立实例。

###### SQL Server 故障转移群集实例

对于 SQL Server 故障转移群集实例，下表列出了受支持的存储类型，以及你可以在 SQL Server 安装过程中配置的默认目录。

| 说明                   | 受支持的存储类型                   | 默认目录                                                     | 建议                                                         |
| :--------------------- | :--------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **数据根目录**         | 共享存储、SMB 文件服务器           | <Drive:>\Program Files\Microsoft SQL Server\  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | SQL Server 安装程序为 SQL Server 目录配置 ACL，并在配置过程中中断继承。 |
| **用户数据库目录**     | 共享存储、SMB 文件服务器           | <Drive:>Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | 用户数据目录的最佳实践取决于工作量和性能要求。               |
| **用户数据库日志目录** | 共享存储、SMB 文件服务器           | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | 确保日志目录有足够的空间。                                   |
| **备份目录**           | 本地磁盘、共享存储、SMB 文件服务器 | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Backup  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | 设置合适的权限以防止数据丢失，并确保 SQL Server 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射驱动器。 |

###### 安全注意事项

安装程序将为 SQL Server 目录配置 ACL 并在配置过程中中断继承。

以下建议适用于 SMB 文件服务器：

- 使用 SMB 文件服务器时， SQL Server 服务帐户必须是域帐户。
- 用于安装 SQL Server 的帐户应对用作数据目录的 SMB 文件共享文件夹拥有完全控制 NTFS 权限。
- 用于安装 SQL Server 的帐户应具有对 SMB 文件服务器的 SeSecurityPrivilege 特权。 若要授予此特权，请使用文件服务器上的“本地安全策略”控制台将 SQL Server 安装帐户添加到 **“管理审核和安全日志”** 策略中。 在“本地安全策略”控制台中，可以在“用户权限分配”部分中的“本地策略”下找到此设置。

###### 注意事项

- 向现有安装添加功能时，既不得更改以前安装的功能的位置，也不得为新功能指定位置。
- 如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 不要将此对话框中的目录分与其他 SQL Server 实例中的目录。 还请在 SQL Server 实例中安装 数据库引擎 和 Analysis Services 组件，以分隔目录。
- 在下列情况下，无法安装程序文件和数据文件：
  - 在可移动磁盘驱动器上
  - 在使用压缩的文件系统上
  - 在系统文件所在的目录上
  - 在故障转移群集实例的映射网络驱动器上



##### “数据库引擎配置 - TempDB”页

此页可用于指定 SQL Server 数据库引擎 的 tempdb 数据和日志文件位置、大小、增长设置和文件数量。 根据安装类型，支持的存储可能包括本地磁盘、共享存储或 SMB 文件服务器。

若要将 SMB 文件共享指定为目录，您必须手动键入支持的 UNC 路径。 不支持转到 SMB 文件共享。 下面的示例展示了受支持的 SMB 文件共享 UNC 路径格式：

```
\\<ServerName>\<ShareName>\....
```

###### SQL Server 独立实例的数据目录和日志目录

对于SQL Server 独立实例，下表列出了受支持的存储类型，以及你可以在使用安装程序期间配置的默认目录。

| 说明         | 受支持的存储类型                    | 默认目录                                                     | 建议                                                         |
| :----------- | :---------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **数据目录** | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data | SQL Server 安装程序为 SQL Server 目录配置 ACL，并在配置过程中中断继承。  tempdb 目录的最佳做法取决于工作负荷和性能需求。 若要跨多个卷分散数据文件，请指定多个文件夹或驱动器。 |
| **日志目录** | 本地磁盘、SMB 文件服务器、共享存储* | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data | 确保日志目录有足够的空间。                                   |

*尽管共享磁盘受支持，但不建议将共享磁盘用于 SQL Server 独立实例。

###### SQL Server 故障转移群集实例的数据和日志目录

对于 SQL Server 故障转移群集实例，下表列出了受支持的存储类型，以及你可以在 SQL Server 安装过程中配置的默认目录。

| 说明                | 受支持的存储类型                   | 默认目录                                                     | 建议                                                         |
| :------------------ | :--------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **tempdb 数据目录** | 本地磁盘、共享存储、SMB 文件服务器 | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\Data  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | SQL Server 安装程序为 SQL Server 目录配置 ACL，并在配置过程中中断继承。  请确保指定的一个或多个目录（如果指定了多个文件）对所有群集节点都有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，SQL Server 资源将无法联机。 |
| **tempdb 日志目录** | 本地磁盘、共享存储、SMB 文件服务器 | <Drive:>\Program Files\Microsoft SQL Server\MSSQL*nn*.<InstanceID>\MSSQL\Data  **提示**：如果你选择“群集磁盘选择”页上的“共享磁盘”，系统默认选择第一个共享磁盘。 如果未在“群集磁盘选择”页上进行任何选择，此字段默认为空白。 | 用户数据目录的最佳实践取决于工作量和性能要求。  确保指定的目录对所有群集节点都有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，SQL Server 资源将无法联机。  确保日志目录有足够的空间。 |

###### UI 元素列表

根据工作负荷和要求配置 **tempdb** 的设置。 下列设置适用于 **tempdb** 数据文件：

- “文件数” 是 **tempdb**的数据文件总数。 默认值是 8 和安装程序检测到的逻辑内核数中的较小值。 作为一般准则，如果逻辑处理器数小于或等于 8，则使用与逻辑处理器数相同的数据文件数。 如果逻辑处理器数大于 8，请指定 8 个数据文件。 如果存在争用，请以 4（逻辑处理器数上限）为倍数增加数据文件数，直到争用减少到可接受的水平，或请更改工作负荷或代码。
- **初始大小(MB)** ：每个 tempdb 数据文件的初始大小（以 MB 为单位）。 默认值为 8 MB（对于 SQL Server Express 为 4 MB）。 SQL Server 2017 (14.x) 引入的最大初始文件大小为 262,144 MB (256 GB)。 SQL Server 2016 (13.x) 的初始文件大小上限为 1024MB。 所有 **tempdb** 数据文件初始大小相同。 由于 tempdb**** 在 SQL Server 每次启动或进行故障转移时都会重新创建，因此请指定与工作负荷正常运行所需大小接近的大小。 若要在启动过程中进一步优化 tempdb 创建，请启用[数据库即时文件初始化](https://docs.microsoft.com/zh-cn/sql/relational-databases/databases/database-instant-file-initialization?view=sql-server-ver15)。
- **总初始大小(MB)** ：所有 tempdb 数据文件的累积大小。
- **自动增长(MB)** ：每个 tempdb 数据文件在空间不足时自动增长的空间量（以 MB 为单位）。 在 SQL Server 2016 (13.x) 及更高版本中，所有数据文件都按此设置中指定的量同时增长。
- **总自动增长 (MB)** 是每个自动增长事件的累积大小。
- **数据目录**：显示保留 tempdb 数据文件的所有目录。 当存在多个目录时，以循环方式将数据文件放置在目录中。 例如，如果你创建 3 个目录，并指定 8 个数据文件，那么数据文件 1、4 和 7 在第一个目录中创建。 数据文件 2、5 和 8 在第二个目录中创建。 数据文件 3 和 6 在第三个目录中创建。
- 若要添加目录，请选择“添加…”。
- 若要删除目录，请依次选择目录和“删除”。

“tempdb 日志文件”是日志文件名。 此文件是自动创建的。 下列设置仅适用于 **tempdb** 日志文件：

- **初始大小 (MB)** 是 **tempdb** 日志文件的初始大小。 默认值为 8 MB（对于 SQL Server Express 为 4 MB）。 SQL Server 2017 (14.x) 引入的最大初始文件大小为 262,144 MB (256 GB)。 SQL Server 2016 (13.x) 的初始文件大小上限为 1024MB。 由于 tempdb**** 在 SQL Server 每次启动或进行故障转移时都会重新创建，因此请指定与工作负荷正常运行所需大小接近的大小。 若要在启动过程中进一步优化 tempdb 创建，请启用[数据库即时文件初始化](https://docs.microsoft.com/zh-cn/sql/relational-databases/databases/database-instant-file-initialization?view=sql-server-ver15)。

   备注

  tempdb 使用最小日志记录。 无法备份 tempdb 日志文件。 它在 SQL Server 每次启动或群集实例进行故障转移时重新创建。

- **自动增长 (MB)** 是 **tempdb** 日志以 MB 为单位的增长量。 默认值 64 MB 在初始化期间创建最优数量的虚拟日志文件。

   备注

  tempdb 日志文件不使用数据库即时文件初始化。

- “日志目录” 是其中创建 **tempdb** 日志文件的日志目录。 只有一个 tempdb 日志目录。

###### 安全注意事项

安装程序为 SQL Server 目录配置 ACL，并在配置过程中中断继承。

以下建议适用于 SMB 文件服务器：

- 使用 SMB 文件服务器时， SQL Server 服务帐户必须是域帐户。
- 如果帐户用于安装 SQL Server，应对用作数据目录的 SMB 文件共享文件夹拥有完全控制 NTFS 权限。
- 用于安装 SQL Server 的帐户应具有对 SMB 文件服务器的 SeSecurityPrivilege 特权。 若要授予此特权，请使用文件服务器上的“本地安全策略”控制台将 SQL Server 安装帐户添加到 **“管理审核和安全日志”** 策略中。 在“本地安全策略”控制台中，可以在“用户权限分配”部分中的“本地策略”下找到此设置。

 备注

如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 此对话框中的任何目录都不应与其他 SQL Server实例的目录共享。 数据库引擎 实例中的Analysis Services和 SQL Server 组件也应安装到单独的目录。

###### 另请参阅

- [配置 Windows 服务帐户和权限](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15)
- [文件服务器上的共享权限和 NTFS 权限](https://docs.microsoft.com/zh-cn/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)



##### “数据库引擎配置 - MaxDOP”页

“最大并行度(MaxDOP)”决定了一个语句最多可以使用多少个处理器。 SQL Server 2019 (15.x) 引入了在安装过程中配置此选项的功能。 SQL Server 2019 (15.x) 还可以根据内核数自动为服务器检测建议的 MaxDOP 设置。

如果在安装过程中跳过此页，默认 MaxDOP 值就是此页中显示的建议值，而不是旧版本 (0) 的默认 数据库引擎 值。 你还可以在此页上手动配置这一设置，并在安装后修改这一设置。

###### UI 元素列表

- “最大并行度 (MaxDOP)”是在并行执行一个语句期间使用的最大处理器数的值。 默认值遵循[配置服务器配置选项“最大并行度”](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option?view=sql-server-ver15#Guidelines)中的最大并行度准则。



##### “数据库引擎配置 - 内存”页

“最小服务器内存”决定了 SQL Server 数据库引擎 将用于缓冲池和其他缓存的内存下限。 默认值和建议值均为 0。 若要详细了解“最小服务器内存”的影响，请参阅[内存管理体系结构指南](https://docs.microsoft.com/zh-cn/sql/relational-databases/memory-management-architecture-guide?view=sql-server-ver15#effects-of-min-and-max-server-memory)。

“最大服务器内存”决定了 SQL Server 数据库引擎 将用于缓冲池和其他缓存的内存上限。 根据现有系统内存，默认值为 2,147,483,647MB，计算出的建议值遵循独立 SQL Server 实例的[服务器内存配置选项](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-ver15#manually)中的内存配置准则。 若要详细了解“最大服务器内存”的影响，请参阅[内存管理体系结构指南](https://docs.microsoft.com/zh-cn/sql/relational-databases/memory-management-architecture-guide?view=sql-server-ver15#effects-of-min-and-max-server-memory)。

如果在安装过程中跳过此页，使用的“最大服务器内存”默认值为 数据库引擎 默认值 (2,147,483,647MB)。 选中“建议”**** 单选按钮后，即可在此页上手动配置这些设置，并在安装后修改这些设置。 有关详细信息，请参阅 [服务器内存配置选项](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-ver15)。

###### UI 元素列表

**默认**：默认情况下，此单选按钮处于选中状态，并将“最小服务器内存”和“最大服务器内存”设置设为 数据库引擎 默认值。

**建议**：必须选中此单选按钮，才能接受计算出的建议值，或将计算出的值更改为用户配置的值。

**最小服务器内存(MB)** ：若要从计算出的建议值更改为用户配置的值，请输入“最小服务器内存”值。

**最大服务器内存(MB)** ：若要从计算出的建议值更改为用户配置的值，请输入“最大服务器内存”值。

**单击此处接受用于 SQL Server 数据库引擎的建议内存配置**：选中此复选框，可以接受此服务器上计算出的建议内存配置。 如果“建议”单选按钮处于选中状态，而此复选框处于未选中状态，那么安装程序将无法继续运行。



##### “数据库引擎配置 - FILESTREAM”页

使用此页可针对此 SQL Server 2019 (15.x)安装启用 FILESTREAM。 FILESTREAM 通过将 varbinary(max) 二进制大型对象 (BLOB) 数据作为文件存储在 NTFS 文件系统中，将 SQL Server 数据库引擎与此文件系统集成在一起。 Transact-SQL 语句可插入、更新、查询、搜索和备份 FILESTREAM 数据。 Microsoft Win32 文件系统接口提供对数据的流访问权限。

###### UI 元素列表

**为 Transact-SQL 访问启用 FILESTREAM**：选中此项可针对 Transact-SQL 访问启用 FILESTREAM。 必须先选中此复选框，然后才能配置其他选项。

**为文件 I/O 流访问启用 FILESTREAM**：选中此项可针对 FILESTREAM 启用 Win32 流访问。

**Windows 共享名**：输入用来存储 FILESTREAM 数据的 Windows 共享名。

**允许远程客户端拥有对 FILESTREAM 数据的流访问权限**：选中这个复选框可允许远程客户端访问此服务器上的 FILESTREAM 数据。

###### 另请参阅

- [启用和配置 FILESTREAM](https://docs.microsoft.com/zh-cn/sql/relational-databases/blob/enable-and-configure-filestream?view=sql-server-ver15)
- [sp_configure (Transact-SQL)](https://docs.microsoft.com/zh-cn/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql?view=sql-server-ver15)



##### “数据库引擎配置 - 用户实例”页

“用户实例”页可用于：

- 为没有管理员权限的用户单独生成数据库引擎实例。
- 将用户添加到管理员角色中。

###### 选项

**启用用户实例**：默认处于启用状态。 若要禁用“启用用户实例”，请取消选中此复选框。

用户实例也称为子实例或客户端实例，是由父实例（作为服务运行的主实例，如 SQL Server ）代表用户生成的 SQL Server Express实例。 用户实例作为用户进程在该用户的安全上下文下运行。 用户实例与父实例和计算机上运行的其他任何用户实例隔离开来。 用户实例功能亦称为“以普通用户身份运行 (RANU)”。

 备注

在使用安装程序期间预配为 sysadmin 固定服务器角色成员的登录名在模板数据库中预配为管理员。 除非遭删除，否则它们是用户实例的 sysadmin 固定服务器角色成员。

**将用户添加到 SQL Server 管理员角色中**：默认处于禁用状态。 若要将当前安装程序用户添加到 SQL Server 管理员角色中，请选中此复选框。

作为 BUILTIN\Administrators 成员的 Windows Vista 用户在连接到 SQL Server Express 时，不会自动添加到 sysadmin 固定服务器角色中。 只有已显式添加到服务器级别管理员角色中的 Windows Vista 用户才能管理 SQL Server Express。 Built-In\Users 组成员可以连接到 SQL Server Express 实例，但他们执行数据库任务的权限有限。 因此，对于从旧版 Windows 的 BUILTIN\Administrators 和 Built-In\Users 继承 SQL Server Express 权限的用户，必须在 Windows Vista 上运行的 SQL Server Express 实例中显式获得管理权限。

若要在安装程序结束后更改用户角色，请使用 [SQL Server Management Studio](https://docs.microsoft.com/zh-cn/sql/relational-databases/security/authentication-access/join-a-role?view=sql-server-ver15) 或 [TRANSACT-SQL](https://docs.microsoft.com/zh-cn/sql/t-sql/statements/alter-role-transact-sql?view=sql-server-ver15)。



#### 2.2.4 SQL Server数据库引擎

**适用于：**![是](https://docs.microsoft.com/zh-cn/sql/includes/media/yes-icon.png?view=sql-server-ver15)SQL Server（所有支持的版本）-仅限 Windows

##### 1. 概述

数据库引擎 的 SQL Server 组件是用于存储、处理数据和保证数据安全的核心服务。 数据库引擎 提供受控的访问和快速事务处理，以满足企业中要求极高、大量使用数据的应用程序的要求。

SQL Server 支持在同一台计算机上最多存在 50 个 数据库引擎 实例。 若要创建典型 SQL Server 安装，请参阅[使用安装向导安装 SQL Server（安装程序）](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup?view=sql-server-ver15)。

 重要

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 SQL Server ，则必须使用对远程共享具有读取和执行权限的域帐户。



##### 2. 功能

在 **SQL Server 安装向导的“要安装的组件”页上选择** 数据库引擎” SQL Server 时，将安装下列功能：

- 数据库引擎
- [SQL Server 复制](https://docs.microsoft.com/zh-cn/sql/relational-databases/replication/sql-server-replication?view=sql-server-ver15) - 可选组件

- [机器学习服务](https://docs.microsoft.com/zh-cn/sql/machine-learning/install/sql-machine-learning-services-windows-install?view=sql-server-ver15)（R 和 Python）以及[语言扩展](https://docs.microsoft.com/zh-cn/sql/language-extensions/install/install-sql-server-language-extensions-on-windows?view=sql-server-ver15) (Java) - 是一个可选组件

- 全文搜索 - 是一个可选组件

- Data Quality Services - 一个可选组件

   备注

  在此版本中，在安装程序中选中“Data Quality Services”复选框不会安装 Data Quality Services (DQS) 服务器。 您必须执行其他安装后步骤以安装 DQS 服务器。 有关详细信息，请参阅 [Install Data Quality Services](https://docs.microsoft.com/zh-cn/sql/data-quality-services/install-windows/install-data-quality-services?view=sql-server-ver15)。

- [针对外部数据的 PolyBase 查询服务](https://docs.microsoft.com/zh-cn/sql/relational-databases/polybase/polybase-guide?view=sql-server-ver15) - 可选组件。 从 SQL Server 2019 开始，还可以使用用于 HDFS 数据源的 Java 连接器。

下列附加功能是许多典型用户应用场景的可选项：

- 数据质量客户端
- Integration Services
- 连接组件
- 编程模型
- 管理工具
- Management Studio
- 文档组件

 备注

默认情况下，不会将示例数据库和示例代码作为 SQL Server 安装程序的一部分进行安装。 若要安装示例数据库和示例代码，请参阅 [Microsoft SQL Server 示例](https://docs.microsoft.com/zh-cn/sql/sample/microsoft-sql-server-samples?view=sql-server-ver15)。 请参阅 [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843) 上的旧示例。



##### 3. 另请参阅

[SQL Server 2017 的各版本和支持的功能](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2017?view=sql-server-ver15)
[计划 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/sql-server/install/planning-a-sql-server-installation?view=sql-server-ver15)
[高可用性解决方案 (SQL Server)](https://docs.microsoft.com/zh-cn/sql/sql-server/failover-clusters/high-availability-solutions-sql-server?view=sql-server-ver15)
[使用安装向导升级 SQL Server（安装程序）](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup?view=sql-server-ver15)



#### 2.2.5 使用安装向导安装 SQL Server（安装程序）

**适用于：**![是](https://docs.microsoft.com/zh-cn/sql/includes/media/yes-icon.png?view=sql-server-ver15)SQL Server（所有支持的版本）-仅限 Windows

本文介绍如何使用安装向导安装 SQL Server。 它适用于 SQL Server 2016 (13.x) 和 SQL Server 2017 (14.x)。

本文介绍了使用 SQL Server 安装程序安装向导来安装新 SQL Server 实例的分步过程。 此安装向导提供了一个用于安装所有 SQL Server 组件的功能树，这样你就不必逐个安装这些组件了。 若要逐个安装 SQL Server 组件，请参阅[安装 SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server?view=sql-server-ver15#individual-component-installation)。

有关安装 SQL Server 的其他方法，请参阅：

- [从命令提示符安装 SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-2016-from-the-command-prompt?view=sql-server-ver15)
- [使用配置文件安装 SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-2016-using-a-configuration-file?view=sql-server-ver15)
- [使用 SysPrep 安装 SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-using-sysprep?view=sql-server-ver15)
- [新建 SQL Server 故障转移群集（安装程序）](https://docs.microsoft.com/zh-cn/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-ver15)
- [使用安装向导升级 SQL Server（安装程序）](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup?view=sql-server-ver15)



##### 获取安装介质

SQL Server 的下载位置由版本决定：

- “SQL Server Enterprise、Standard 和 Express Edition” 已获授权，可供生产之用。 对于企业版和标准版，请联系软件供应商获取安装媒体。 你可以在 [Microsoft 采购网站](https://www.microsoft.com/sql-server/)上找到采购信息和 Microsoft 合作伙伴目录。
- [最新免费版本](https://www.microsoft.com/sql-server/sql-server-downloads)。



##### 先决条件

安装 SQL Server 前，请先审阅[计划 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/sql-server/install/planning-a-sql-server-installation?view=sql-server-ver15)。

 备注

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 SQL Server ，则必须使用对远程共享具有读取和执行权限的域帐户。



##### 安装 SQL Server 2019

1. 插入 SQL Server 安装介质， 然后双击根文件夹中的 **Setup.exe**。 若要从网络共享进行安装，请先在共享中找到根文件夹，再双击“Setup.exe”。

2. 安装向导将运行 SQL Server 安装中心。 若要新建 SQL Server 安装，请依次选择左侧导航区域中的“安装”和“新建 SQL Server 独立安装或向现有安装添加功能”。

3. 在“产品密钥”页中，选择选项来指明是要安装 SQL Server 免费版本，还是要安装有 PID 密钥的生产版本。 有关详细信息，请参阅 [SQL Server 2017 的各版本和支持的功能](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-version-15?view=sql-server-ver15)。

   若要继续操作，请选择“下一步”。

4. 在“许可条款”页中，审阅许可协议。 如果同意，请选中“我接受许可条款和[隐私声明](https://privacy.microsoft.com/privacystatement)”复选框，再选择“下一步”。

    备注

   如果输入了企业服务器/CAL 许可证产品密钥，且计算机上有 20 多个物理内核，或者在启用超线程时有 40 个逻辑内核，则安装过程中会显示警告。 要继续安装，请选择“选中此框确认此限制或单击‘返回/取消’输入支持操作系统最大处理器数的企业内核产品许可证”复选框，或者单击“返回”并输入支持操作系统最大处理器数的许可证密钥 。

    备注

   SQL Server 传输有关安装体验的信息，以及其他使用情况和性能数据，以帮助 Microsoft 改进产品。 若要详细了解 SQL Server 数据处理和隐私控制，请参阅[隐私声明](https://privacy.microsoft.com/privacystatement)和[将 SQL Server 配置为向 Microsoft 发送反馈](https://docs.microsoft.com/zh-cn/sql/sql-server/sql-server-customer-feedback)。

5. 在“全局规则”页中，如果没有规则错误，安装程序会自动跳转到“产品更新”页。

6. 如果未在依次转到“控制面板” > “所有控制面板项” > “Windows 更新” > “更改设置”后选中“Microsoft 更新”复选框，接下来会转到“Microsoft 更新”页。 选中“Microsoft 更新”复选框会将计算机设置更改为，在扫描是否有 Windows 更新时，扫描所有 Microsoft 产品的最新更新。

7. “产品更新”页显示最新 SQL Server 产品更新。 如果未发现任何产品更新，安装程序就不会显示此页，并自动跳转到“安装安装程序文件”页。

8. 在“安装安装程序文件”页中，安装程序显示安装程序文件的下载、提取和安装进度。 如果找到了安装程序更新，且你指定包括它，也会安装此更新。 如果未找到任何更新，安装程序将自动进行。

9. 在“安装规则”页中，安装程序会检查是否有可能会在运行安装程序时发生的潜在问题。 如果检查到故障，请选择“状态”列中的项，以了解详细信息。 否则，请选择“下一步”。

10. 如果这是首次在计算机上安装 SQL Server，安装程序会跳过“安装类型”页，并直接转到“功能选择”页。 如果系统中已安装有 SQL Server，你可以使用“安装类型”页来选择是执行新安装，还是向现有安装添加功能。 若要继续操作，请选择“下一步”。

11. 在“功能选择”页上，选择要安装的组件。 例如，要安装新的 SQL Server 数据库引擎 实例，请选择“数据库引擎服务”。

    选择功能名称后， **“功能说明”** 窗格中会显示每个组件组的说明。 您可以选中任意一些复选框。 有关详细信息，请参阅 [SQL Server 2016 版本和组件](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2016?view=sql-server-ver15)或 [SQL Server 2017 版本和组件](https://docs.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2017?view=sql-server-ver15)。

    **“所选功能的必备组件”** 窗格中将显示所选功能的必备组件。 安装程序在本过程后面所述的安装步骤中安装尚未安装的系统必备。

    也可以使用“功能选择”页底部的字段，指定共用组件的自定义目录。 若要更改共用组件的安装路径，请更新对话框底部字段中的路径，或选择“浏览”转到安装目录。 默认安装路径为 C:\Program Files\Microsoft SQL Server\nnn\ \。

     备注

    为共享组件指定的路径必须是绝对路径。 文件夹不能压缩或加密。 不支持映射驱动器。

    SQL Server 对共享功能使用两个目录：

    - 共享功能目录
    - 共享功能目录 (x86)

     备注

    为以上每个选项指定的路径必须不同。

12. 如果所有规则都通过，“功能规则”页会自动跳转。

13. 在“实例配置”页中，指定是要安装默认实例，还是命名实例。 有关详细信息，请参阅[实例配置](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#instance-configuration-page)。

    - **实例 ID**：默认情况下，实例名称用作实例 ID。 此 ID 用于标识 SQL Server 实例的安装目录和注册表项。 对于默认实例和命名实例，行为是相同的。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认实例 ID，请在“实例 ID”文本框中指定其他值。

       备注

      典型 SQL Server 独立实例（无论是默认实例，还是命名实例）不会使用非默认实例 ID 值。

      所有 SQL Server Service Pack 和升级都适用于 SQL Server 实例的每个组件。

    - **已安装实例**：此网格显示正在运行安装程序的计算机上的 SQL Server 实例。 如果计算机上已经安装了一个默认实例，则必须安装 SQL Server的命名实例。

    安装程序的其余工作流视你已为安装指定的功能而定。 你可能不会看到所有页，具体视你的选择而定。

14. 自 SQL Server 2019 (15.x) 起，PolyBase 不再要求在安装此功能前预先在计算机上安装 Oracle JRE 7 Update 51（最低版本）。 选择安装 Polybase 功能会将“Java 安装位置”页添加到 SQL Server 安装程序，并显示在“实例配置”页之后 。 在“Java 安装位置”页上，可以选择安装 SQL Server 2019 (15.x) 安装随附的 Azul Zulu Open JRE，也可以提供已在计算机上安装的另一个 JRE 或 JDK 的位置。

15. 自 SQL Server 2019 (15.x) 起，Java 已经添加了语言扩展。 选择安装 Java 功能会将“Java 安装位置”页添加到 SQL Server 安装程序对话框窗口，并显示在“实例配置”页之后 。 在“Java 安装位置”页上，可以选择安装 SQL Server 2019 (15.x) 安装随附的 Zulu Open JRE，也可以提供已在计算机上安装的另一个 JRE 或 JDK 的位置。

16. 使用“服务器配置 - 服务帐户”页指定 SQL Server 服务的登录帐户。 你在此页中配置的实际服务取决于你已选择安装的功能。 若要详细了解配置设置，请参阅[安装向导帮助](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#serverconfig)。

    可以为所有 SQL Server 服务分配相同的登录帐户，也可以单独配置各个服务帐户。 还可以指定是自动启动、手动启动还是禁用服务。 建议单独配置服务帐户，以提供每个服务的最小特权。 请务必向 SQL Server 服务授予完成任务所必需的最低权限。 有关详细信息，请参阅[配置 Windows 服务帐户和权限](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-ver15)。

    若要为此 SQL Server 实例中的所有服务帐户指定同一个登录帐户，请在此页底部的字段中提供凭据。

     重要

    不要使用空密码。 请使用强密码。

     备注

    自 SQL Server 2016 (13.x) 起，选中“向 SQL Server 数据库引擎服务授予执行卷维护任务权限”复选框，可以让 SQL Server 数据库引擎服务帐户使用[数据库即时文件初始化](https://docs.microsoft.com/zh-cn/sql/relational-databases/databases/database-instant-file-initialization?view=sql-server-ver15)。

    使用“服务器配置 - 排序规则”页指定数据库引擎和 Analysis Services 的非默认排序规则。 有关详细信息，请参阅[排序规则和 Unicode 支持](https://docs.microsoft.com/zh-cn/sql/relational-databases/collations/collation-and-unicode-support?view=sql-server-ver15)。

17. 使用“数据库配置 - 服务器配置”页指定以下各个选项：

    - **安全模式**：为 SQL Server 实例选择“Windows 身份验证”或“混合模式身份验证”。 如果选择“混合模式身份验证”，必须为内置 SQL Server 系统管理员帐户提供强密码。

      在设备与 SQL Server 成功建立连接后，用于 Windows 身份验证和混合模式身份验证的安全机制是相同的。 有关详细信息，请参阅[“数据库引擎配置 - 服务器配置”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#serverconfig)。

    - **SQL Server 管理员**：必须为 SQL Server 实例指定至少一个系统管理员。 若要添加用于运行 SQL Server 安装程序的帐户，请选择“添加当前用户”。 若要在系统管理员列表中添加或删除帐户，请先选择“添加”或“删除”，再编辑对 SQL Server 实例拥有管理员权限的用户、组或计算机列表。

    使用“数据库引擎配置 - 数据目录”页指定非默认安装目录。 若要安装到默认目录，请选择“下一步”。

     重要

    如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 此对话框中的任何目录都不应与其他 SQL Server实例的目录共享。

    有关详细信息，请参阅[“数据库引擎配置 - 数据目录”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#datadir)。

    使用“数据库引擎配置 - TempDB”页配置 tempdb 的文件大小、文件数、非默认安装目录和文件增长设置。 有关详细信息，请参阅[“数据库引擎配置 - TempDB”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#tempdb)。

    使用“数据库引擎配置 - MaxDOP”页指定最大并行度。 此设置决定了一个语句可以在执行期间使用多少个处理器。 系统自动在安装期间计算建议值。

     备注

    仅自 SQL Server 2019 (15.x) 起，才能在“设置”中使用此页。

    有关详细信息，请参阅[“数据库引擎配置 - MaxDOP”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)。

    使用“数据库引擎配置 - 内存”页，指定此 SQL Server 实例在启动后使用的“最小服务器内存和“最大服务器内存”值。 可以使用默认值、计算出的建议值，也可以在选择“推荐”选项后手动指定你自己的值。

     备注

    仅自 SQL Server 2019 (15.x) 起，才能在“设置”中使用此页。

    有关详细信息，请参阅[“数据库引擎配置 - 内存”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)。

    使用“数据库引擎配置 - FILESTREAM”页为 SQL Server 实例启用 FILESTREAM。 有关详细信息，请参阅[“数据库引擎配置 - FILESTREAM”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#database-engine-configuration---filestream-page)。

18. 使用“Analysis Services - 帐户预配”页指定服务器模式，以及对 Analysis Services 拥有管理员权限的用户或帐户。 服务器模式决定了哪些内存和存储子系统用于服务器。 不同的解决方案类型在不同的服务器模式下运行。 如果计划在服务器上运行多维数据集数据库，请选择默认服务器模式选项“多维和数据挖掘”。

    必须为 Analysis Services 指定至少一个系统管理员：

    - 若要添加正在运行 SQL Server 安装程序的帐户，请选择“添加当前用户”。
    - 若要在系统管理员列表中添加或删除帐户，请先选择“添加”或“删除”，再编辑对 Analysis Services 拥有管理员权限的用户、组或计算机列表。

    若要详细了解服务器模式和管理员权限，请参阅[“Analysis Services 配置 - 帐户预配”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#analysis-services-configuration---account-provisioning-page)。

    编辑完列表后，选择“确定”。 验证配置对话框中的管理员列表。 在列表是完整后，单击“下一步”。

    使用“Analysis Services - 数据目录”页指定非默认安装目录。 若要安装到默认目录，请选择“下一步”。

     重要

    安装 SQL Server 时，如果你为 INSTANCEDIR 和 SQLUSERDBDIR 指定相同的目录路径，SQL Server 代理和全文搜索不会启动，因为缺少权限。

    如果指定非默认安装目录，请确保安装文件夹对此 SQL Server 实例是唯一的。 此对话框中的任何目录都不应与其他 SQL Server实例的目录共享。

    有关详细信息，请参阅[“Analysis Services 配置 - 数据目录”页](https://docs.microsoft.com/zh-cn/sql/sql-server/install/instance-configuration?view=sql-server-ver15#analysis-services-configuration---data-directories-page)。

19. 使用“Distributed Replay 控制器配置”页指定要向其授予 Distributed Replay 控制器服务管理权限的用户。 拥有管理权限的用户可以不受限制地访问 Distributed Replay 控制器服务。

    - 若要向正在运行 SQL Server 安装程序的用户授予 Distributed Replay 控制器服务访问权限，请选择“添加当前用户”按钮。
    - 若要向其他用户授予 Distributed Replay 控制器服务访问权限，请选择“添加”按钮。
    - 若要撤消 Distributed Replay 控制器服务访问权限，请选择“删除”按钮。
    - 若要继续操作，请选择“下一步”。

20. 使用“Distributed Replay 客户端配置”页指定要向其授予 Distributed Replay 客户端服务管理权限的用户。 拥有管理权限的用户可以不受限制地访问 Distributed Replay 客户端服务。

    - “控制器名称”是可选选项。 默认值是 <*blank*>。 输入客户端计算机用来与 Distributed Replay 客户端服务通信的控制器的名称：
      - 如果已设置控制器，请在配置每个客户端时输入控制器名称。
      - 如果尚未设置控制器，可以将控制器名称保留为空白。 但是，您必须在 **“客户端配置”** 文件中手动输入控制器名称。
    - 为 Distributed Replay 客户端服务指定 **“工作目录”** 。 默认工作目录为 <*drive letter*>:\Program Files\MicrosoftSQL Server\DReplayClient\WorkingDir\。
    - 为 Distributed Replay 客户端服务指定 **“结果目录”** 。 默认结果目录为 <*drive letter*>:\Program Files\MicrosoftSQL Server\DReplayClient\ResultDir\。
    - 若要继续操作，请选择“下一步”。

21. “准备安装”页显示你在使用安装程序期间指定的安装选项的树状视图。 在此页中，安装程序指明“产品更新”功能是启用还是禁用，以及最终更新版本。

    若要继续操作，请选择“安装”。 SQL Server 安装程序先安装选定功能的系统必备，再安装选定功能。

22. 在安装过程中，“安装进度”页显示状态更新，以便你能在安装程序继续运行时监视安装进度。

23. 安装完成后， **“完成”** 页会提供指向安装摘要日志文件以及其他重要说明的链接。

     重要

    运行完安装程序后，请务必阅读安装向导中的消息。 有关详细信息，请参阅[查看和读取 SQL Server 安装程序日志文件](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files?view=sql-server-ver15)。

    若要完成 SQL Server 安装过程，请单击“关闭”。

24. 如果系统指示你重启计算机，请立即重启。



##### 后续步骤

[配置新 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/database-engine-instances-sql-server?view=sql-server-2017)。

为了减少系统的可攻击外围应用， SQL Server 有选择地安装和启用了一些关键服务和功能。 有关详细信息，请参阅[外围应用配置](https://docs.microsoft.com/zh-cn/sql/relational-databases/security/surface-area-configuration?view=sql-server-ver15)。



##### 另请参阅

- [验证 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/validate-a-sql-server-installation?view=sql-server-ver15)
- [修复失败的 SQL Server 安装](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/repair-a-failed-sql-server-installation?view=sql-server-ver15)
- [查看和读取 SQL Server 安装程序日志文件](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files?view=sql-server-ver15)
- [使用安装向导升级 SQL Server（安装程序）](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup?view=sql-server-ver15)
- [从命令提示符安装 SQL Server](https://docs.microsoft.com/zh-cn/sql/database-engine/install-windows/install-sql-server-2016-from-the-command-prompt?view=sql-server-ver15)



## 3. 安装数据库系统

### 3.1 选择安装类型

​	点击安装程序，需要选择SQL Server 2019的安装类型：选择基本即可。

![1.png](http://panzy25.ticp.io:4000/images/2020/09/08/1.png)

<center>图15</center>



​	允许接受Microsoft SQL Server的许可条款：

![2.png](http://panzy25.ticp.io:4000/images/2020/09/08/2.png)

<center>图16</center>



​	确定SQL Server 2019的安装位置：

![3.png](http://panzy25.ticp.io:4000/images/2020/09/08/3.png)

<center>图17</center>



​	等待下载安装包，需要确认磁盘拥有足够的安装空间，否则可能会导致安装失败：

![4.png](http://panzy25.ticp.io:4000/images/2020/09/08/4.png)

<center>图18</center>



​	下载完成后，需要等待安装，这些步骤都是由安装程序自动触发的，只需要等待即可：

![5.png](http://panzy25.ticp.io:4000/images/2020/09/08/5.png)

<center>图19</center>



​	等待一段时间之后，会出现已成功完成安装的指示：

![6.png](http://panzy25.ticp.io:4000/images/2020/09/08/6.png)

<center>图20</center>



​	下载完成后，需要使用SQL Server Management Studio对SQL Server进行管理：

![7.png](http://panzy25.ticp.io:4000/images/2020/09/08/7.png)

<center>图21</center>



​	等待SSMS安装完成：

![10.png](http://panzy25.ticp.io:4000/images/2020/09/08/10.png)

<center>图22</center>



​	SSMS安装后可以看到安装程序的相关提醒：

![11.png](http://panzy25.ticp.io:4000/images/2020/09/08/11.png)

<center>图23</center>



​	此时重新回到SQL Server的安装界面，点击自定义，可以看到安装程序开始检测计算机的安装状态：

![8.png](http://panzy25.ticp.io:4000/images/2020/09/08/8.png)

<center>图24</center>



​	根据提示重新启动计算机，会发现打开SQL Server安装程序后，会提示已经安装了一个实例。如果愿意安装一个相同的实例，只需要继续点击基本即可。我暂时不需要2个实例，所以选择了自定义，在自定义中，根据提示按照默认设置账户密码和其他相关设置，即可完成安装SQL Server：

![9.png](http://panzy25.ticp.io:4000/images/2020/09/08/9.png)

<center>图25</center>



​	打开Microsoft SQL Server Management Studio，可以看到有关数据库的信息选项，进行身份验证即可完成登陆：

​	<center>![12.png](http://panzy25.ticp.io:4000/images/2020/09/08/12.png)</center>

<center>图26</center>

## 4. 总结

​	整个安装过程虽然总体来说比较顺利，但是还是有一些波折，查阅了很多资料。例如在重启后如何继续安装，自定义安装数据库路径等等。这些问题在下一次的作业中会详细阐述。