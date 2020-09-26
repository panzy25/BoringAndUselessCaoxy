# 数据库第二次作业:

<center>sql server安装配置</center>



> written by panzy25, 18372046
>
> on Typora
>
> Based on Markdown language 

[TOC]

## 1. 作业简述

​	基于曹老师对于SQL Server版本号的建议，我对SQL Sever在另外一台电脑上进行了重新的安装。所有有关第一次作业的内容将在此处作简要介绍。

​	本次作业主要安装 SQL Server 2008 express和SQL Server Management Studio Express，并通过SQL Server配置管理器配置服务实现数据库连接使用。本次安装并未选择完整版的SQL Server 2008 express而是分别独立安装SQL Server 2008 express和SQL Server Management Studio Express，目的是更清晰地理解SQL Server的各组件与服务，在环境配置的实践过程中完整掌握SQL Server的结构框架，加深对SQL Server 2008 express功能的认识。本次报告将首先从理论角度比较SQL Server的不同版本，阐述本次实验选择安装SQL Server 2008 express的理由；其次介绍SQL Server Management Studio Express，从支持SQL Server 2008 express的角度说明SQL Server Management Studio Express的功能与作用；然后梳理安装SQL Server 2008 express和SQL Server Management Studio Express的正确流程，说明SQL Server 2008 express的相关环境配置方法要求；最后专门设置实验板块以实验验证和探究的方式，通过修改并查看SQL Server 实例名及实例根目录，辨析并修改SQL Server服务账户 ，以混合验证方式设置并修改sa登录密码，添加登录名并设置用户名映射与权限等实验进一步理解SQL Server安装配置的组件与服务的内在联系，从理论和实践角度加深对SQL Server的熟悉程度。

​	本次报告在第一次安装报告重点阐述安装过程中功能选择、实例配置、服务器配置以及数据库引擎配置等的理论与实际作用的基础上，拓展实验设计板块，从实例、服务器账户、身份验证方式、登录名与用户名等角度突出SQL Server各组件与服务的内在联系；主要目的是加深对SQL Server的内在功能关系理解，在实验设计中熟悉安装好的SQL Server软件各功能与设置属性的操作，同时探索安装过程中各项设置的实际关联，将理论运用于实践亲身验证并自我拓展。



## 2. 版本选择

​	这一部分从三个方面介绍SQL Server的相关理论知识并阐述本次实验选择安装SQL Server 2008 express的理由；首先总体介绍SQL Server不同版本基本情况并进行对比；其次重点介绍本次实验安装的版本SQL Server 2008 express，包括其基本配置、优缺点与定位；最后阐述版本选择的理由并说明SQL Server 2008 express的安装与配置要求。

### 2.1 版本对比

SQL Server 是Microsoft 公司推出的关系型数据库管理系统，具有使用方便可伸缩性好与相关软件集成程度高等优点，使用集成的商业智能 (BI)工具提供了企业级的数据管理，并可以构建和管理用于业务的高可用和高性能的数据应用程序。[<sup>1</sup>](#refer-anchor-1)

#### 2.1.1 SQL Server 2008 不同版本

​	如下表所示是SQL Server 2008 express的各版本介绍：[<sup>2</sup>](#refer-anchor-2)

| SQL  Server 2008 Developer（x86、x64 和 IA64）               | SQL  Server 2008 Developer 支持开发人员构建基于 SQL Server 的任一种类型的应用程序。 它包括 SQL Server 2008 Enterprise 的所有功能，但有许可限制，只能用作开发和测试系统，而不能用作生产服务器。SQL Server 2008 Developer 是构建和测试应用程序的人员的理想之选。 可以升级 SQL Server 2008 Developer 以将其用于生产用途。 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 工作组（x86 和 x64）                                         | SQL  Server Workgroup 是运行分支位置数据库的理想选择，它提供一个可靠的数据管理和报告平台，其中包括安全的远程同步和管理功能。 |
| Web（x86、x64）                                              | 对于为从小规模至大规模 Web 资产提供可扩展性和可管理性功能的 Web 宿主和网站来说，SQL Server 2008 Web 是一项总拥有成本较低的选择。 |
| SQL  Server Express（x86 和 x64）  SQL  Server Express with Tools（x86 和 x64）  SQL  Server Express with Advanced Services（x86 和 x64） | SQL  Server Express 数据库平台基于 SQL Server 2008。 它也可用于替换 Microsoft Desktop Engine (MSDE)。 SQL  Server Express 与 Visual Studio 集成，从而开发人员可以轻松开发功能丰富、存储安全且部署快速的数据驱动应用程序。  SQL  Server Express 免费提供，且可以由 ISV 再次分发（视协议而定）。SQL Server Express 是学习和构建桌面及小型服务器应用程序的理想选择， 也是独立软件供应商、非专业开发人员和热衷于构建客户端应用程序的人员的最佳选择。  如果您需要使用更高级的数据库功能，则可以将 SQL Server Express 无缝升级到更复杂的 SQL Server 版本。 |
| Compact  3.5 SP1 (x86)  Compact  3.1 (x86)                   | SQL  Server Compact 3.5 免费提供，是生成用于基于各种 Windows 平台的移动设备、桌面和 Web 客户端的独立和偶尔连接的应用程序的嵌入式数据库理想选择。 |

<center>表1</center>

​	综合上表所述，SQL Server 2008 express适用于个人学习，能满足基本使用需要。本次安装的SQL Server 2008 express是SQL Server 2008中最基础的一版，需要单独增加SSMS Express组件支持使用。

#### 2.1.2 SQL Server 2008 r2

​	SQL Server 2008 r2为任何规模的应用提供完备的信息平台以及可管理的，熟悉的自服务商业智能(BI)工具。它支持大规模数据中心与数据仓库，支持平滑建立与扩展应用到云端与微软的应用平台紧密集成。[<sup>3</sup>](#refer-anchor-3)SQL Server 2008 r2对比SQL Server 2008引进了一系列新功能帮助各种规模的业务从信息中获取更多价值。经过改进的SQL Server 2008 R2增强了开发能力，提高了可管理性，强化了商业智能及数据仓库。

### 2.2 SQL Server 2008 Express简介

#### 2.2.1 SQL Server 2008 Express基本配置

  MicrosoftSQL Server 2008 Express 是基于 MicrosoftSQL Server 的数据库平台，支持SQL Server 的大多数功能，如下表所示：[<sup>4</sup>](#refer-anchor-4)

| 存储过程                                   | SQL  Server 配置管理器          |
| ------------------------------------------ | ------------------------------- |
| 视图                                       | 复制（仅作为订阅服务器）        |
| 触发器                                     | 高级查询优化器                  |
| 游标                                       | SMO/RMO                         |
| sqlcmd 和  osql 实用工具                   | 与  Visual Studio 2005 集成。   |
| 快照隔离级别                               | Service  Broker（仅作为客户端） |
| 本机 XML 支持，包括 XQuery 架构和 XML 架构 | SQL CLR                         |
| Transact-SQL  语言支持                     | 多个活动的结果集 (MARS)         |
| 专用管理员连接                             | 导入/导出向导                   |

<center>表2</center>

#### 2.2.2 SQL Server 2008 express优缺点

##### （1）优点

​	SQL Server Express 简化了开发功能丰富的数据驱动应用程序的过程，提高了存储安全性并加快了部署速度。SQL Server Express 的所有版本均可免费下载，并可在协议的许可下重新分发。每一版本既可充当客户端数据库，又可充当基本服务器数据库。[<sup>5</sup>](#refer-anchor-5)由于SQL Server 2008 express支持任意一版 SQL Server Express ，是独立软件供应商 (ISV)、服务器用户、非专业开发人员、Web 开发人员、网站主人以及创建客户端应用程序的业余爱好者的理想之选。

##### （2）缺点

​	数据库的大小限制：SQL Server 2005 Express和SQL Server 2008 Express 数据库的大小限制最大为 4GB，最新版本的SQL Server 2008 R2 Express 数据库的大小限制最大为10G。这个大小的限制只在数据文件上，事务日志大小则不受此限。只能使用一个 CPU 来运算，这在多个 CPU 的电脑上会造成浪费。可使用的存储器量最高只有 1GB。没有 SQL Agent，若要做调度服务必须自己写程序。

​	一方面SQL Server express免费便于安装使用；另一方面它继承了多数的SQL Server功能与特性，还可和商用程序一起使用的小型数据库管理系统，适合使用在小型的网站或者小型的桌面型应用程序，满足当前SQL Server学习使用的需要；所以本次安装选择SQL Server 2008 express，当然如果后续需要SQL Server更专业的功能与服务可以较容易地升级更新为新的版本。

### 2.3 安装要求

​	SQL Server 2008 express相较于SQL Server 2008 express r2需要单独增添SSMS express的安装，虽然Microsoft SQL Server 2008 R2提供完整的企业级技术与工具，但是本次实验选择分别独立安装SQL Server 2008 express和SQL Server Management Studio Express，目的是更清晰地理解SQL Server的各组件与服务，熟悉SQL Server express的配置。



## 3. SQL SERVER 2008 EXPRESS安装

​	这一部分将介绍SQL Server 2008 express的安装流程，重点解释安装中的“功能选择”，“实例配置”，“数据库引擎”以及“服务器配置”，同时就安装中遇到的问题分享解决方法。

### 3.1 安装程序下载运行

​	此次安装选择的版本为Microsoft sql server 2008 express,根据我的电脑是64位win10系统的条件，在Microsoft官网的下载中心下载安装程序SQLEXPR_X64_CHS.exe；成功下载后直接在下载路径D：sql server 2008 express对应的物理目录下双击运行SQLEXPR_X64_CHS.exe安装程序。

![image001.png](http://panzy25.ticp.io:4000/images/2020/09/20/image001.png)

<center>图1</center>



<img src="http://panzy25.ticp.io:4000/images/2020/09/20/image004.jpg" alt="image004.jpg" style="zoom:150%;" />

<center>图2</center>

### 3.2 全新sql server 独立安装

​	进入SQL Server 安装中心进入安装界面并选择安装类型：全新SQL Server独立安装或向现有安装添加功能。

![image005.png](http://panzy25.ticp.io:4000/images/2020/09/20/image005.png)

<center>图3</center>

![image007.png](http://panzy25.ticp.io:4000/images/2020/09/20/image007.png)

<center>图4</center>



### 3.3 安装程序支持规则

​	安装程序支持规则是sql server安装开始之前必要的检查工作，以避免安装过程可能出现的问题；主要分为两步：首先为确认开始安装之前，检查安装SQL Server安装程序支持文件可能发生的问题；其次为确认并安装SQL Server安装程序支持文件及组件后，再次进行规则检查；检查失败的规则需要更正以继续安装。此次安装过程中我遇到“重新启动计算机”和“Windows防火墙”亮相规则检查不通过的问题，查阅资料通过修改注册表和暂时关闭防火墙解决了问题。下面将展示安装程序支持规则的正确步骤，重点介绍规则检测失败的解决方案。

#### 3.3.1 安装程序支持规则步骤

![image009.png](http://panzy25.ticp.io:4000/images/2020/09/20/image009.png)

<center>图5</center>

![image011.png](http://panzy25.ticp.io:4000/images/2020/09/20/image011.png)

<center>图6</center>

​	SQL Server对应版本密钥输入以验证实例，由于此次实验安装的SQL Server 2008 express是免费版本不用输入密钥检测，直接点击下一步。

![image013.png](http://panzy25.ticp.io:4000/images/2020/09/20/image013.png)

<center>图7</center>

![image015.png](http://panzy25.ticp.io:4000/images/2020/09/20/image015.png)

<center>图8</center>

![image017.png](http://panzy25.ticp.io:4000/images/2020/09/20/image017.png)

<center>图9</center>

#### 3.3.2 规则检测失败解决方案

​	此次安装遇到的检查失败主要是“重新启动计算机”和“Windows防火墙”规则失败。

##### （1）重新启动计算机

![image019.png](http://panzy25.ticp.io:4000/images/2020/09/20/image019.png)

<center>图10</center>

​	一般情况下“重新启动计算机”规则失败根据安装提示重新启动系统即可解决，但是此次实验中我尝试重新启动计算机再次安装仍显示失败。

![image021.png](http://panzy25.ticp.io:4000/images/2020/09/20/image021.png)

<center>图11</center>

​	通过查阅资料了解到：注册表中的`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager`存放的是当前系统会话的快照，而`PendingFileRenameOperations`记录的是一个未成功进行的文件更名操作，应用程序如SQL Server在安装时可能会使用这个键值，记录在安装过程中对临时文件的操作，如果在安装进程启动时就发现这个键值存在，它就认为上一个安装程序没有完成，从而拒绝继续自身的安装进程。[<sup>6</sup>](#refer-anchor-6)所以删除注册表中的`PendingFileRenameOperations`也是解决“重新启动计算机”规则失败的一种方法。

![image023.png](http://panzy25.ticp.io:4000/images/2020/09/20/image023.png)

<center>图12</center>

打开注册表编辑器找到`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`

![image025.png](http://panzy25.ticp.io:4000/images/2020/09/20/image025.png)

<center>图13</center>

​	删除`Session Manager`的`PendingFileRenameOperations`记录

![image027.png](http://panzy25.ticp.io:4000/images/2020/09/20/image027.png)

<center>图14</center>

​	重新运行安装程序支持规则检测——“重新启动计算机”通过

##### （2）Windows防火墙

![image027.png](http://panzy25.ticp.io:4000/images/2020/09/20/image027.png)

<center>图15</center>

​	Windows防火墙显示警告可能会组织SQL Server的安装，解决方法是安装过程中暂时关闭防火墙，安装成功后重新开启防火墙功能。

![image029.png](http://panzy25.ticp.io:4000/images/2020/09/20/image029.png)

<center>图16</center>

​	网络和Internet设置中进入Windows 防火墙安全中心

![image031.png](http://panzy25.ticp.io:4000/images/2020/09/20/image031.png)

<center>图17</center>

<img src="http://panzy25.ticp.io:4000/images/2020/09/21/-1.png" alt="-1.png" style="zoom:150%;" />

<center>图18</center>

​	重新运行规则检查Windows防火墙通过。

### 3.4 功能选择

​	功能选择板块是对安装的SQL Server进行功能配置，主要分为实例功能和共享功能；“实例功能”表示为每个实例安装一次的组件，“共享功能”是指给定计算机上所有实例所共有的功能。[<sup>7</sup>](#refer-anchor-7)由于数据库要放在服务器上运行，所以约定不同的服务器引擎就是不同的实例，实例可以在不同的机器上，也可以在相同的机器上，在相同的机器上时，实例名不能相同；每个SQL Server数据库引擎实例各有一套不为其他实例共享的系统及用户数据库。[<sup>8</sup>](#refer-anchor-8)同时功能选择板块还需要设置共享功能目录，即共享实例的存放位置：单台计算机上所有实例使用的公共文件安装在以下文件夹中：<drive>:\Program Files\Microsoft SQL Server\nnn\。其中 <drive> 是安装组件的驱动器号，默认值通常为驱动器 C；<nnn> 标识版本。[<sup>9</sup>](#refer-anchor-9)此次安装中全选SQL Server 2008 express的所有实例功能和共享功能，并保持默认的功能共享目录。

​	下面将分别说明SQL Server 2008 express的实例功能和共享功能，并拓展介绍SQL Server其它版本可提供的实例功能和共享功能，以阐述此次实验中功能选择“全选”的理由与作用，同时说明express版本相较其它版本的特点及定位，了解SQL Server的各项功能服务的联系。

<img src="http://panzy25.ticp.io:4000/images/2020/09/21/image034.jpg" alt="image034.jpg" style="zoom:150%;" />

<center>图19</center>

#### 3.4.1 实例功能

​	数据库引擎服务是SQL Server 实例功能中的核心功能，同时也是SQL Server 2008 express支持的主要实例功能。SQL Server 数据库引擎 包括数据库引擎（用于存储、处理和保护数据安全的核心服务）、复制、全文搜索、用于管理关系数据和 XML 数据的工具以及 Data Quality Services (DQS) 服务器。

| 数据库引擎             | 用于存储、处理和保护数据的核心服务                           |
| ---------------------- | ------------------------------------------------------------ |
| 复制                   | 复制是一组技术，它将数据和数据库对象从一个数据库复制和分发到另一个数据库，然后在数据库之间进行同步以保持一致性。 |
| 全文搜索               | 全文搜索提供了针对 SQL Server 表中基于纯字符的数据发出全文查询的功能。 |
| Data Quality  Services | Data Quality  Services (DQS) 是一种数据清理解决方案，它不仅能让你发现数据源中不一致和不正确的数据，还能提供计算机辅助且交互式方法来清理数据。选中此复选框将安装 DQS 服务器。完成 SQL Server 安装之后，您必须运行 DQSInstaller.exe 文件，才能完成 DQS 服务器安装。如果你已安装 SQL Server 的默认实例，则此文件位于 `C:\Program  Files\MicrosoftSQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn` 下。 |

<center>表3</center>

​	SQL Server 2008 Express 基于 SQL Server，并支持该产品的大多数数据库引擎功能，express版本在数据库引擎服务中可选数据库引擎和复制，此次安装中全选了SQL Server 2008 Express能提供的全部实例功能即数据库引擎服务。

#### 3.4.2 共享功能

​	由一台计算机上的所有 SQL Server 实例共享的功能安装在一个目录中，SQL Server 2008 express支持的共享功能主要为SQL 客户端连接 SDK，SQL 客户端连接 SDK为数据库应用程序开发包括 SQL Server Native Client (ODBC/OLE DB) SDK。

| 名称                               | 功能                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| Open Database  Connectivity (ODBC) | 开放数据库连接，使用SQL语法操纵关系数据的国际标准. 要操纵数据的话就需要通过有微软或其他厂商提供的ODBC drivers.[<sup>10</sup>](#refer-anchor-10) |
| OLE DB                             | 对象链接和嵌入数据库，微软的low-level的访问数据的接口.       |
| SQL Server Native  Client          | 本地客户端，用于 OLE DB 和 ODBC 的独立数据访问应用程序编程接口 (API) |

<center>表4</center>

​	OLE DB Provider跟ODBC Driver是类似的, Provider对OLE DB Consumer暴露DataSource。ODBC旨在提供对多平台环境中的SQL数据的访问。OLE DB旨在提供对OLE组件对象模型（COM）环境中的所有类型的数据的访问。[<sup>11</sup>](#refer-anchor-11)SQL Server Native Client 是在 SQL Server 2005 中引入的用于 OLE DB 和 ODBC 的独立数据访问应用程序编程接口 (API)，也即本地客户端。SQL Server Native Client 将 SQL OLE DB 访问接口和 SQL ODBC 驱动程序组合成一个本机动态链接库 (DLL)，它可用于创建新应用程序或增强现有应用程序，使这些应用程序能够利用在 SQL Server 2005 中引入的功能，例如多个活动结果集 (MARS)、用户定义数据类型 (UDT)、查询通知、快照隔离和 XML 数据类型支持。[<sup>12</sup>](#refer-anchor-12)

​    默认情况下，共享组件安装到` %Program Files%Microsoft SQL Server\ `中。若要更改安装路径，请单击“浏览”按钮。如果更改一个共享组件的安装路径，则要同时更改其他共享组件的安装路径。后续安装会将共享组件安装到与原始安装相同的位置。



#### 3.4.3 拓展：SQL Server其它共享与实例功能介绍

​	虽然SQL Server Express 支持 SQL Server 的大多数功能，但是由于SQL Server Express是SQL Server的免费微缩版本，所以其并不支持常见基本需求以外的功能与组件服务。如下图列出SQL Server express 支持的主要功能。

![image035.png](http://panzy25.ticp.io:4000/images/2020/09/21/image035.png)

<center>图21</center>

​	SQL Server express不支持的组件包括：Reporting Service、Notification Service、Integration Service，Analysis Service、全文搜索、OLAP 服务/数据挖掘；带有工具的SQL Server express（SQL Server express with tools）增添了SQL Server Management Studio 的基本安装：有助于轻松管理 SQL Server Express 数据库的图形管理工具；具有高级服务功能的SQL Server express（SQL Server express with Advanced Services）增添了SQL Server Management Studio 的基本安装：有助于轻松管理 SQL Server Express 数据库的图形管理工具，Reporting Services，BI Development Studio：这提供了用于创建报表的报表创建和设计集成环境，全文搜索：用于搜索文本密集型数据的功能强大的搜索引擎。[<sup>13</sup>](#refer-anchor-13)下面介绍SQL Server具有的其它实例功能与共享功能。



##### （1）实例功能

| Analysis Services    | Analysis Services 包括用于创建和管理联机分析处理 (OLAP) 以及数据挖掘应用程序的工具。 |
| -------------------- | ------------------------------------------------------------ |
| Reporting Services   | Reporting Services 包括用于创建、管理和部署表格报表、矩阵报表、图形报表以及自由格式报表的服务器和客户端组件。Reporting Services 还是一个可用于开发报表应用程序的可扩展平台。 |
| Integration Services | Integration Services 是一组图形工具和可编程对象，用于移动、复制和转换数据。 |

<center>表5</center>

##### （2）共享功能

| Reporting Services – SharePoint                     | Reporting Services SharePoint 模式是一种基于服务器的应用程序，用于创建、管理报表并将报表传递到电子邮件、多种文件格式和基于 Web 的交互格式。SharePoint 模式将报表查看和报表管理体验与 SharePoint 产品集成在一起。 |
| --------------------------------------------------- | ------------------------------------------------------------ |
| 用于 SharePoint 产品的  Reporting Services 外接程序 | 用于 SharePoint 产品的  Reporting Services 外接程序包含管理和用户界面组件，以便将 SharePoint 产品与 SharePoint 模式下的 Reporting Services 报表服务器进行集成。 |
| 数据质量客户端                                      | Data Quality Client 是一个独立的应用程序，它连接到 DQS 服务器，并提供一个直观的图形用户界面来执行数据清除和数据匹配操作，以及在  DQS 中执行管理任务。 |
| 客户端工具连接                                      | 客户端工具包括用于在客户端和服务器之间进行通信的组件，其中包括用于  DB-Library、OLEDB for OLAP、ODBC、ADODB 和 ADOMD+ 的各种网络库。 |
| 客户端工具 SDK                                      | 包括包含针对程序员的资源的软件开发包。                       |
| Master Data Services                                | Master Data Services 是一个平台，用于将整个组织内不同系统中的数据集成到单一主数据源，以确保准确性和进行审核。Master Data Services 选项安装 Master Data  Services 配置管理器、程序集、Windows PowerShell 管理单元以及 Web 应用程序和服务的文件夹和文件。 |

<center>表6</center>

### 3.5 实例配置

实例配置板块作用为设置默认实例或者命名实例的实例ID与实例根目录。由于安装 SQL Server 将安装一个或多个单独的实例，无论是默认实例还是命名实例都有自己的一组程序文件和数据文件，同时还有在计算机上的所有 SQL Server 实例之间共享的一组公共文件。所以为了隔离每个组件的安装位置，将为给定 SQL Server实例中的每个组件都生成一个唯一的实例 ID。[<sup>14</sup>](#refer-anchor-14)此次实验在实例配置板块主要设置默认实例并按照个人需要修改了实例根目录。

每个 SQL Server 实例都由一组在排序规则及其他选项方面具有特定设置的非重复服务组成。目录结构、注册表结构和服务名称均反映了在 SQL Server 安装期间创建的实例名称和特定实例 ID。[<sup>15</sup>](#refer-anchor-15)默认情况下，实例名称用作实例 ID。默认实例和命名实例的默认方式都是如此。

#### 3.5.1 默认实例

SQL实例，实际上就是SQL服务器引擎；在一台计算机上，可以安装多个SQL SERVER，每个SQL SERVER就可以理解为是一个实例。在一台计算机上安装第一个SQLSERVER且命名设置保持默认，则这个实例就是默认实例。一台计算机上最多只有一个默认实例，也可以没有默认实例。默认实例名与计算机名相同，但不称为“local”；一般情况下，如果要访问本机上的默认SQL服务器实例，使用计算机名、(local)、localhost、127.0.0.1、. 、本机IP地址，都可以达到相同的目的。但如果要访问非本机的SQL服务器，那就必须使用计算机/实例名的办法。计算机名是可以修改的，但修改后对默认实例无影响,即默认实例随计算机名的改变而改变。[<sup>16</sup>](#refer-anchor-16)此次安装SQL Server 2008 express是在此电脑上的第一次安装，选择实例设置为默认实例即可。

SQL Server 安装过程中，为每个服务器组件生成一个实例 ID。 此 SQL Server 版本中的服务器组件分别是数据库引擎、Analysis Services和 Reporting Services。

默认实例ID使用以下格式构造：

- 对于数据库引擎采用的是 MSSQL，后面依次跟有主版本号、下划线和次版本号（如果适用）、一个句点以及实例名。

- 对于Analysis Services采用的是 MSAS，后面依次跟有主版本号、下划线和次版本号（如果适用）、一个句点以及实例名。

- 对于Reporting Services采用的是 MSRS，后面依次跟有主版本号、下划线和次版本号（如果适用）、一个句点以及实例名。[<sup>17</sup>](#refer-anchor-17)

此次安装的SQL Server 2008 express的默认实例名称为SQLExpress。

#### 3.5.2 命名实例

​	如果计划在同一台计算机上安装多个实例应使用命名实例，SQL Server 支持在单个服务器或处理器上存在多个 SQL Server 实例，但只能有一个实例为默认实例，所有其他实例必须为命名实例。SQL Server 安装期间可指定一个非默认实例 ID，可为实例 ID 指定任何值，但应避免使用特殊字符和保留关键字。命名实例的命名规则类似默认实例，只需要修改自定义的实例名称。实例名限制为16个字符且不区分大小写，实例名中的第一个字符必须是字母，可接受的字母为 Unicode 标准 2.0 定义的那些字母，包括拉丁字符 a-z、A-Z 和其他语言中的字母字符。后续字符可以是 Unicode 标准 2.0 定义的字母、源于基本拉丁语或其他国家/地区书写符号的十进制数字、美元符号 ($) 或者下划线 (_)。实例名称中不允许含有空格或其他特殊字符，也不允许存在反斜杠 (\\)、逗号 (,)、冒号 (:)、分号 (;)、单引号 (')、and 符 (&) 和 at 符 (@)。[<sup>18</sup>](#refer-anchor-168)

​	例如：在服务器中的服务名称：SQL Server 2017 默认实例，为 MSSQL14.MSSQLSERVER，名“MyInstance”的 SQL Server 2017 命名实例，为 MSSQL14.MyInstance。连接到查询分析器或探查器的连接字符串：默认实例可以使用:“.”(点)、“(local)”、“计算机名称”；而命名实例需要使用计算机名\实例名。

#### 3.5.3 实例根目录

​	如果用户选择更改默认安装目录，则不使用 `<Program Files>\MicrosoftSQL Server`，而使用 自定义路径\MicrosoftSQL Server。 不支持以下划线()开头或者包含数字符号(#)或美元符号($)的实例 ID。一个共享组件的安装路径还会更改其他共享组件的安装路径，后续安装会将非实例识别组件安装到与原始安装相同的目录。

​	由于SQL Server 为每个服务组件生成一个实例ID，所以根据实例ID命名规则给出此次安装版本SQL Server 2008 express选择的功能组件的安装路径：[<sup>19</sup>](#refer-anchor-19)

| 数据库引擎服务器组件                     | ` \Program  Files\MicrosoftSQL Server\MSSQL14.<InstanceID>\  ` |
| ---------------------------------------- | ------------------------------------------------------------ |
| 客户端组件（bcp.exe 和 sqlcmd.exe 除外） | `<Install Directory>\140\Tools\  `                           |
| 所有 SQL Server                          | ` <drive>:\Program  Files\Microsoft SQL Server\nnn\Shared\  ` |
| 客户端组件（bcp.exe 和 sqlcmd.exe）      | `  <安装目录>\Client  SDK\ODBC\110\Tools\Binn  `             |

<center>表7</center>

![image037.png](http://panzy25.ticp.io:4000/images/2020/09/21/image037.png)

<center>图22</center>

​	选择默认实例，并修改实例根目录到D盘自定义文件夹

### 3.6 磁盘空间要求

​	磁盘空间要求是在安装过程中供用户检查并确认拥有足够的磁盘空间支持SQL Server的进一步安装，此次安装中我的电脑具有充足的空间，所以点击“下一步”确认继续安装。

![image039.png](http://panzy25.ticp.io:4000/images/2020/09/21/image039.png)

<center>图23</center>

### 3.7 服务器配置

​	服务器配置可以为所有的 SQL Server 服务分配相同的登录帐户，也可以分别配置各个服务帐户；同时能指定服务是自动启动、手动启动还是禁用的。

#### 3.7.1 服务账户

- NT Authority\System，系统内置账号，对本地系统拥有完全控制权限；在工作组模式下，该账户不能访问网络资源；通常用于服务的运行，不需要密码。

- NT Authority\Network Service，系统内置账号，比 SYSTEM 账户权限要小，可以访问有限的本地系统资源；在工作组模式下，该账户能够以计算机的凭据来访问网络资源，默认为远程服务器的 EVERYONE 和 AUTHENTICATED USER 组的身份；通常用于服务运行，不需要密码。

- NT Authority\Local Service，系统内置账号，比NETWORK SERVICE账户权限要小，可以访问有限的本地系统资源；在工作组模式下，该账户只能以匿名方式访问网络资源；通常用于服务的运行，不需要密码。[<sup>20</sup>](#refer-anchor-20)

#### 3.7.2 单独配置SQL Server服务账户

​	SQL Server支持为每项 SQL Server 服务设置一个登录用户名和密码并设置相应服务的启动类型。如下表列出部分SQL Server服务账户配置[<sup>21</sup>](#refer-anchor-21)

| **选择此服务**     | **为其配置身份验证设置的主体**                               |
| ------------------ | ------------------------------------------------------------ |
| SQL Server Agent   | 运行作业、监视 SQL Server 并可自动处理管理任务的服务。  此服务没有默认登录帐户。  默认的启动类型为“手动”。 |
| SQL Server         | SQL Server 数据库引擎。  此服务没有默认登录帐户。  默认的启动类型为“自动”。 |
| SQL Server Browser | SQL Server Browser 是向客户端计算机提供 SQL Server 连接信息的名称解析服务。多个 SQL Server 和 Integration Services 实例共享此服务。  默认登录帐户为 NT  Authority\Local service 且无法更改。  默认的启动类型为“自动”。 |

<center>表8</center>

在 SQL Server Express 实例和 SQL Server Express with Advanced Services 实例上 SQL Server Agent 服务已禁用。默认情况下，对于故障转移群集安装和命名实例，SQL Server Browser 设置为在安装程序完成后自动启动。[<sup>22</sup>](#refer-anchor-22)

#### 3.7.3 对SQL Server服务使用启动账户

若要启动并运行 SQL Server 中的服务，则每个服务都必须有一个在安装过程中配置的用户帐户。用户帐户可以是内置系统帐户、本地用户帐户或域用户帐户。除具有用户帐户外，每个服务还有用户可控制的三种可能的启动状态：

- 已禁用 服务已安装但当前未运行。

- 手动 服务已安装，但仅当另一个服务或应用程序需要该服务的功能时才启动。

- 自动服务由操作系统自动启动。[<sup>23</sup>](#refer-anchor-23)

| SQL Server         | SQL Server Express：Domain  User、Local System、Network  Service1  所有其他版本：Domain User、Local System、Network Service | 自动                                         | 已启动  仅当用户选择不自动启动时才停止 |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------- | -------------------------------------- |
| SQL Server Agent   | Domain User、Local  System、Network Service1                 | 手动  仅当用户选择自动启动时才成为“自动”     | 已停止  仅当用户选择自动启动时才启动   |
| SQL Server Browser | Local Service                                                | 已禁用  仅当用户选择自动启动时才成为“自动”。 | 已停止  仅当用户选择自动启动时才启动。 |

<center>表9</center>

​	如图24此次安装选择具有完全控制权限的系统内置账号进行配置，同时从安全性出发选择单独为SQL Server 2008 express各项服务配置账户。由于express版本只提供了对SQL Server Browser服务的配置选择，所以保持SQL Server Browser服务账户并指定服务自动启动。

![image041.png](http://panzy25.ticp.io:4000/images/2020/09/21/image041.png)

<center>图24</center>

### 3.8 数据库引擎配置

​	数据库引擎配置板块主要为数据库引擎指定身份验证模式和管理员，此次安装选择混合验证模式并为内置的SQL Server系统管理员账户设置密码；同时添加用以运行SQL Server安装程序的账户为SQL Server管理员，使其具有无限制的访问权限。

#### 3.8.1 安全模式

此次实验，SQL Server 安装程序设置 sa 登录密码并配合混合模式身份验证，通过指定一个密码可以防止未经授权的访问到的 SQL Server 实例使用sa登录。选择身份验证模式的目的是确定登陆SQL Server的类型，此次实验选择的混合验证模式既支持windows身份验证，即已经登录到 Windows 的用户不必再单独登录到 SQL Server；又支持通过设置登陆密码使用内部身份验证方法验证尝试的SQL Server单独登录。多种数据库服务登陆方式，保证内置SQL Server系统管理员和windows本机主体用户都能访问数据库。

#### 3.8.2 身份验证模式

​	SQL Server登录服务器有两种验证方式，一种是windows身份验证，也就是本机验证，另一种就是SQL Server验证，就是使用账号密码的方式验证。Windows身份验证是默认模式（通常称为集成安全），此SQL Server安全模型与 Windows 高度集成：信任特定Windows 用户和组帐户登录 SQL Server，已经通过身份验证的Windows用户不必提供附加的凭据，也即无密码登陆。混合模式身份验证，必须创建SQL Server登录名，将其存储在SQL Server中且必须在运行时提供SQL Server用户名和密码。SQL Server 使用名为sa（“系统管理员”的缩写）的SQL Server登录进行安装。为 sa 登录分配一个强密码，并且不要在应用程序中使用 sa 登录。sa 登录名会映射到sysadmin固定服务器角色，它对整个服务器有不能撤销的管理凭据。[<sup>24</sup>](#refer-anchor-24)

#### 3.8.3 指定SQL Server管理员

​	必须为 SQL Server 实例至少指定一个 Windows 主体。若要添加用以运行SQL Server安装程序的帐户，单击“当前用户”按钮。若要向系统管理员列表中添加帐户或从中删除帐户，单击“添加”或“删除”，然后编辑将拥有 SQL Server实例的管理员权限的用户、组或计算机的列表。[<sup>25</sup>](#refer-anchor-25)此次实验指定当前用户为SQL Server管理员的windows主体。

![image043.png](http://panzy25.ticp.io:4000/images/2020/09/21/image043.png)

<center>图25</center>

### 3.9 错误和使用情况报告

​	安装配置选择完成进入错误和使用情况报告板块，根据个人需要设置错误和使用情况报告发送、更新等服务。

![image045.png](http://panzy25.ticp.io:4000/images/2020/09/21/image045.png)

<center>图26</center>

### 3.10 安装规则

​	再次进行安装前的规则检查，全部通过无失败警告则进入下一步正式安装。

![image047.png](http://panzy25.ticp.io:4000/images/2020/09/21/image047.png)

<center>图27</center>

### 3.11 安装完成

​	通过安装规则检查并确认安装后正式开始安装，等待一段时间查看安装进度全部完成，并进入最终的安装完成信息板块，SQL Server 2008 express安装顺利完成。

![image051.png](http://panzy25.ticp.io:4000/images/2020/09/21/image051.png)

<center>图28</center>

​	由于SSMS的安装在第一次报告中已经完成，在此处不多赘述。

## 4. 服务配置

​	成功安装SQL Server 2008 express以及SQL Server Management Studio还需要在SQL Server配置管理器进行服务器连接配置。此次实验服务配置主要分为SQL Server服务连接本地数据库和SQL Server网络配置，以保证SQL Server 2008 express基本的正常连接使用。配置完成后需要重启动SQL Server时配置生效。

​	下面将在服务配置步骤中介绍通过启动SQLEXPRESS协议和修改TCP/IP属性进行SQL Server网络配置的正确流程；同时针对此次实验过程中遇到的SQL Server服务无法正常开启的问题：远程调用过程失败，介绍远程调用失败的解决方法。

### 4.1 服务配置步骤

​	为确保安装好的SQL Server能成功连接到本地数据库并开启服务，需要在SQLEXPRESS协议中启用协议并修改TCP/IP的端口。

#### 4.1.1 SQLEXPRESS协议

SQL Server服务器可以同时使用多种协议处理来自于客户端的“各种请求”，每一个客户端只使用一种协议连接到 SQL Server服务器。[<sup>26</sup>](#refer-anchor-26)SQL Server 网络配置中的SQLEXPRESS的协议就是SQL Server可以启用、禁用以及配置SQL SERVER服务器实例的网络协议，以用来与客户端连接并处理请求。

Shared Memory、Named Pipes、和TCP/IP三项协议都是客户端协议，Shared Memory能让客户端连接到同一台电脑上运行的SQL实例[<sup>27</sup>](#refer-anchor-27)；Named PipesNamed Pipe（命名管道）是一种用于局域网的协议。在此协议下，计算机的一部分内存会被某个进程用于向另一个进程传递信息，后者可以是本地进程，也可以是远程的。[<sup>28</sup>](#refer-anchor-28)TCP/IP 是 Internet 上广泛使用的通讯协议，它使得互连网络中，“硬件结构和操作系统各异的”计算机能够进行通信，在SQL Server 中主要用来支持远程连接。VIA是虚拟接口适配器(Virtual Interface Adapter)，用于两个系统极高性能的专业连接，[<sup>29</sup>](#refer-anchor-29)此次安装不需要启用。

SQL Server服务配置需要启用Shared Memory、Named Pipes、和TCP/IP三项协议，维持VIA协议禁用状态。如图配置前Named Pipes和TCP/IP协议都是禁用状态，为了避免了同一台计算机上的客户端和服务器实例之间的“进程间封送(跨越进程边界传送信息之前包装信息的方式)”，需要开启Shared Memory使客户端进程直接访问了服务器存储数据的内存映射文件。为了提高连接速度并增强安全性，需要开启Named Pipes保证在局域网下快速安全的连接。为了使SQL Server 2008 express支持远程连接，需要开启TCP/IP使得SQL Server express在默认允许本机访问情况下也能远程连接。

![image067.png](http://panzy25.ticp.io:4000/images/2020/09/21/image067.png)

<center>图29</center>

​	启用协议。

![image071.png](http://panzy25.ticp.io:4000/images/2020/09/21/image071.png)

<center>图30</center>

#### 4.1.2 TCP/IP属性

​	SQL Server服务器连接配置需要修改TCP/IP的端口，在TCP/IP属性选择IP地址，将IPALL中的 “TCP 动态端口” 设置为空，并设置 “TCP 端口”为 1433。

​	进入TCP/IP属性。

![image073.png](http://panzy25.ticp.io:4000/images/2020/09/21/image073.png)

<center>图31</center>

​	修改TCP端口和TCP动态端口。

![image075.png](http://panzy25.ticp.io:4000/images/2020/09/21/image075.png)

<center>图32</center>

​	配置完成后重新启动SQL Server服务。

![image077.png](http://panzy25.ticp.io:4000/images/2020/09/21/image077.png)

<center>图33</center>

### 4.2 服务配置调试——远程调用失败

​	如图 安装完SQL Server 2008 express和SSMS后进入SQL Server配置管理器查看SQL Server服务出现“远程调用过程失败”的问题。

![image079.png](http://panzy25.ticp.io:4000/images/2020/09/21/image079.png)

<center>图34</center>

​	经过查阅资料发现是由于我的电脑安装的Visual Studio和SQL Server冲突，导致数据库找不到访问地址而带来的连接失败，我在计算机管理中的服务和应用程序中查看到两个不同版本的Microsoft SQL Server Express LocalDB。删除Microsoft SQL Server Express 2019LocalDB，只保留Microsoft SQL Server Express 2008LocalDB，重启SQLSERVER 服务问题得到解决。

![image081.png](http://panzy25.ticp.io:4000/images/2020/09/21/image081.png)

<center>图35</center>

​	进入计算机管理，选择服务和应用程序，在服务中找到SQL Server Express 2019LocalDB并删除，只保留QL Server Express 2008LocalDB.

​	刷新SQL Server服务。

![image083.png](http://panzy25.ticp.io:4000/images/2020/09/21/image083.png)

<center>图36</center>

​	SQL Server 2008 Express 不支持 SQL Server 代理，因此显示 “已停止”。

![image085.png](http://panzy25.ticp.io:4000/images/2020/09/21/image085.png)

<center>图37</center>

## 5. 连接配置

​	安装和配置完成之后连接数据库，打开SQL Server Management Studio使用Windows身份验证输入服务器名称连接数据库。

  与Windows身份验证匹配的服务器名称为电脑名\SQLEXPRESS，可以输入（local SQLEXPRESS，.\SQLEXPRESS，计算机名\SQLEXPRESS。

​	至此SQL Server 2008express安装配置及连接完全成功。

![image089.png](http://panzy25.ticp.io:4000/images/2020/09/21/image089.png)

<center>图38</center>

## 6. 实验设计

### 6.1 查看实例名称及实例根目录

#### 6.1.1 实验目的

​	实例指SQL Server数据库引擎，分为默认实例和命名实例。此次安装过程中选择默认实例并修改了实例根目录，通过此次实验查看实例名称和实例根目录。

#### 6.1.2 实验过程

![image091.png](http://panzy25.ticp.io:4000/images/2020/09/21/image091.png)

<center>图39</center>

#### 6.1.3 实验结果

​	此次实验选择的是默认实例：.\SQLEXPRESS。默认实例名与计算机名相同，但不称为“local”；一般情况下，如果要访问本机上的默认SQL服务器实例，使用计算机名、(local)、localhost、127.0.0.1、. 、本机IP地址，都可以达到相同的目的。但如果要访问非本机的SQL服务器，那就必须使用计算机/实例名的办法。命名实例的命名规则类似默认实例，只需要修改自定义的实例名称。实例名限制为16个字符且不区分大小写，实例名中的第一个字符必须是字母。

​	用户选择更改默认安装目录，则不使用 `<Program Files>\MicrosoftSQL Server`，而使用 `<自定义路径\MicrosoftSQL Server`。 不支持以下划线()开头或者包含数字符号(#)或美元符号($)的实例 ID。

### 6.2 辨析并修改SQL Server服务账户

#### 6.2.1 实验目的

​	要启动SQL Server 的服务需要启动对应的用户帐户，SQL Server 2008 express用户账户分为内置系统帐户和域用户帐户，内置系统帐户细分成三类本地系统帐户、网络服务帐户以及本地服务帐户。[<sup>30</sup>](#refer-anchor-30)本次实验探本地系统账户、本地服务账户、网络服务账户和域用户账户的区别，并设计实验查看并修改当前SQL Server的用户账户即SQL Server 服务的登陆类型。

#### 6.2.2 实验内容

​	用户账户是指设置启动sql server服务的登录身份，内置系统账户是以当前的windows账户登陆，本地用户账户是以服务的方式登录，域用户账户是以远程的Server的身份登陆。[<sup>31</sup>](#refer-anchor-31)用户账户的选择涉及到“安全上下文”和“凭据”的概念， Windows凭据（Credential）其实就是指用户帐户和口令，我们调用一些API只要当前用户存储有目标远程机的权限合适的凭据，则这些API就不会因产生ERROR_ACCESS_DENIED而执行失败。安全上下文（Security context）是指在一个系统中有效的安全属性或规则。

​	此实验中我们将通过控制面板的服务和SQL Server 配置管理器的SQL Server服务查看并修改SQL Server 的服务登陆类型。

#### 6.2.3 实验过程

​	本地系统选项指定一个不需要密码的本地管理员级别的系统帐户，对本地计算机具有管理员权限的预定义本地帐户，在本地系统帐户的安全上下文中运行的服务向远程服务器提供本地计算机的凭据。在本地系统帐户的安全上下文中运行的服务不能建立身份验证会话，使用该帐户的服务只能通过空会话(没有凭据)来访问网络资源。

​	网络服务帐户是一个特殊的内置帐户，它与通过身份验证的用户帐户类似，网络服务帐户与 Users 组的成员具有相同级别的资源和对象访问权限。以网络服务帐户身份运行的服务将使用计算机帐户的凭据访问网络资源。

​	本地服务帐户是一个特殊的内置帐户，它与通过身份验证的用户帐户类似。本地服务帐户与 Users 组的成员具有相同级别的资源和对象访问权限。如果有个别服务或进程的安全受到威胁，则此有限访问权限有助于保护系统的安全。以本地服务帐户身份运行的服务将以一个没有凭据的空会话形式访问网络资源。

​	域用户帐户是一个使用 Windows 身份验证的域用户帐户，以设置并连接到 SQL Server。Microsoft 建议对 SQL Server 服务使用具有最低权限的域用户帐户，因为 SQL Server 服务不需要管理员帐户特权。在域用户帐户的安全上下文中运行的服务可以访问经过身份验证的用户或特定用户帐户有权访问的远程服务器上的资源，也即必须在域内的一个账号下运行才能访问远程服务器资源，所以使用域账号是比较典型的方式。

​	此次实验选择配置内置系统账户，由于现阶段对SQL Server express的使用与学习限于本地数据库连接访问，所以内置系统账户足以支持本机学习的需要；此次实验通过控制面板的服务板块和SQL Server 配置管理器的SQL Server 服务两种方法修改账户登陆类型。

##### （1）SQL Server 配置管理器

![image093.png](http://panzy25.ticp.io:4000/images/2020/09/21/image093.png)

<center>图40</center>

​	进入SQL Server 配置管理器选择SQL Server服务，选中要修改登陆类型的具体服务（如图选择SQL Server）

![image095.png](http://panzy25.ticp.io:4000/images/2020/09/21/image095.png)

<center>图41</center>

​	进入选中服务的属性，在登陆板块的内置账户栏可以修改内置系统账户类型。

##### （2）控制面板

​	进入管理工具下的服务。

![image097.png](http://panzy25.ticp.io:4000/images/2020/09/21/image097.png)

<center>图42</center>

​	在服务中选择SQL Server的具体服务并进入属性设置。

![image099.png](http://panzy25.ticp.io:4000/images/2020/09/21/image099.png)

<center>图43</center>

​	在属性的登陆栏修改登陆账户。

![image101.png](http://panzy25.ticp.io:4000/images/2020/09/21/image101.png)

<center>图44</center>

#### 6.2.4 实验结果与总结

- NT Authority\System，系统内置账号，对本地系统拥有完全控制权限；在工作组模式下，该账户不能访问网络资源；通常用于服务的运行，不需要密码。

- NT Authority\Network Service，系统内置账号，比 SYSTEM 账户权限要小，可以访问有限的本地系统资源；在工作组模式下，该账户能够以计算机的凭据来访问网络资源，默认为远程服务器的 EVERYONE 和 AUTHENTICATED USER 组的身份；通常用于服务运行，不需要密码。

- NT Authority\Local Service，系统内置账号，比NETWORK SERVICE账户权限要小，可以访问有限的本地系统资源；在工作组模式下，该账户只能以匿名方式访问网络资源；通常用于服务的运行，不需要密码。

- 域用户适合远程服务器连接和多台SQL Server 服务器相互通信，如果在本机进行开发或学习，没必要使用域用户帐户登录模式，因为有时候因为切换不同用户而导致服务不能启动。如果需要使用远程过程调用、复制等功能必须把登录类型改为“域用户帐户”，并输入在远程计算机上配置好的“用户名”和“密码”。此次选择的系统内置账户中的本地系统账户，享有本机所有权限并不需要登陆名和密码，相较网络服务账户和本地服务账户具有更高的访问权限，同时满足本地学习使用的需要不用配置为域用户账户。

### 6.3 混合验证模式设置、修改与登陆

#### 6.3.1 实验目的

​	SQL Server安装过程中选择身份验证模式为混合验证并设置SQL Server “sa”登陆名的密码，混合验证模式同时支持windows身份本机服务器名登陆和SQL Server创建的登录名和密码的形式登陆。此次实验通过分别使用windows身份验证和SQL Server登陆两种方式连接数据库，并查看SQL Server登录名和密码，最终修改sa登录名密码并实现重新成功登陆，以深入理解SQL Server混合身份验证和登陆名密码设置的内在关联。

#### 6.3.2 实验内容

​	分别使用windows身份验证和SQL Server登陆两种方式连接数据库；查看SQL Server登录名和密码；修改sa密码并重新登陆。

#### 6.3.3 实验过程

##### （1）使用SQL Server登陆方式登陆

​	由于在安装过程中选定混合身份验证方式，所以连接数据库时可以使用登录名sa和设定的密码直接登陆。

![image103.png](http://panzy25.ticp.io:4000/images/2020/09/21/image103.png)

<center>图45</center>

​	登陆成功。

![image105.png](http://panzy25.ticp.io:4000/images/2020/09/21/image105.png)

<center>图46</center>

​	 SQL Server方式登录需要输入登录名和密码，而使用Windows身份验证已经过身份验证的 Windows 用户不必提供附加的凭据，即已经登录到 Windows 的用户不必再单独登录到 SQL Server。从Microsoft官网查阅资料：SqlConnection.ConnectionString指定了 Windows 身份验证，无需用户提供用户名或密码。

##### （2）查看SQL Server身份验证方式、登录名及密码

​	登陆进入数据库后可以在“对象资源管理器”——属性——“安全性”中查看并修改身份验证方式，注意修改身份验证方式之后需要退出登陆重新登陆修改才会生效；“安全性”——“登录名”中可以查看当前SQL Server的所有登录名；由于在登录名的属性中无法查看密码，所以如果设定好混合验证方式并设置了sa的密码的情况下忘记密码，可以使用“新建查询”并输入EXECUTE sp_password NULL,‘输入新密码’,‘sa’，设置sa的新密码。

![image107.jpg](http://panzy25.ticp.io:4000/images/2020/09/21/image107.jpg)

<center>图47</center>

​	在安全性中查看服务器身份验证方式。

![image108.png](http://panzy25.ticp.io:4000/images/2020/09/21/image108.png)

<center>图48</center>

​	选择sa并进入属性界面查看密码。

![image112.png](http://panzy25.ticp.io:4000/images/2020/09/21/image112.png)

<center>图49</center>

##### （3）修改sa密码重新登录

​	sa的登录密码可以在sa的属性中修改，注意：修改密码之后需要重启SQL Server修改才能生效。

![image116.png](http://panzy25.ticp.io:4000/images/2020/09/21/image116.png)

<center>图50</center>

​	Sa的登陆属性中的状态表明SQL Server登陆sa是否启用，如图安装时选择的混合验证模式，此次安装的SQL Server express sa的状态是启用。

#### 6.3.4 实验结果与总结

​	身份验证是指通过提交服务器评估的凭据以登录到主体请求访问的 SQL Server 的过程，身份验证可以确定接受身份验证的用户或进程的标识。此次实验通过进入SQL Server 属性的安全性查看SQL Server 的身份验证方式，并针对sa修改密码重新登陆；在实现SQL Server身份验证方式和登录密码修改的过程中，理解了SQL Server安全性的身份验证实现，同时实践摸索出SQL Server 内在账户设置与联系；当然实验操作中也积累了如修改设置需要重新启动SQL Server服务等经验。



## 7. 总结与感想

​	本次实验独立安装了SQL Server 2008 express和SQL Server Management Studio并成功完成服务器的配置，实现了SQL Server express与数据库的连接；在实验过程中了解了SQL Server express的各项组件与服务。但是本次安装只是使用SQL Server的基本准备，缺乏对SQL Server真正的实践操作；同时安装停留在SQL Server基本功能的配置，并没有深入理解SQL Server功能与服务的内在联系。为此我将在第二次的报告中重视对SQL Server express的实际使用，重点理解SQL Server的内在原理并在操作中加以体会，特别将设计实验就SQL Server的身份验证进行登录名修改与添加的尝试，查找资料了解SQL Server关系型数据库的实现机理以及实践关于使用SQL Server的一些基本操作。



## 8. 参考文献

<div id="refer-anchor-1"></div>  
- [1] [https://baike.baidu.com/item/Microsoft%20SQL%20Server/2947866?fromtitle=sql%20server&fromid=245994&fr=aladdin](https://baike.baidu.com/item/Microsoft%20SQL%20Server/2947866?fromtitle=sql%20server&fromid=245994&fr=aladdin)

  <div id="refer-anchor-2"></div> 

- [2] [https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms144275(v=sql.100)](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms144275(v=sql.100))

<div id="refer-anchor-3"></div>

- [3] [https://zhidao.baidu.com/question/1989084926209323307.html](https://zhidao.baidu.com/question/1989084926209323307.html)

<div id="refer-anchor-4"></div>

- [4] [https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms165588(v=sql.100)](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms165588(v=sql.100))

<div id="refer-anchor-5"></div>

- [5] [https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms165588(v=sql.100)](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/ms165588(v=sql.100))

<div id="refer-anchor-6"></div>

- [6] [https://blog.csdn.net/cupid0051/article/details/6967323](https://blog.csdn.net/cupid0051/article/details/6967323)

<div id="refer-anchor-7"></div>

- [7] [https://www.cnblogs.com/xdot/p/5286279.html](https://www.cnblogs.com/xdot/p/5286279.html)

<div id="refer-anchor-8"></div>

- [8] [https://zhidao.baidu.com/question/1640313408271084100.html](https://zhidao.baidu.com/question/1640313408271084100.html)

<div id="refer-anchor-9"></div>

- [9] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017)

<div id="refer-anchor-10"></div>

- [10] [https://www.cnblogs.com/awpatp/archive/2011/05/16/2047846.html](https://www.cnblogs.com/awpatp/archive/2011/05/16/2047846.html)

<div id="refer-anchor-11"></div>

- [11] [https://www.jianshu.com/p/71399e2d40cb](https://www.jianshu.com/p/71399e2d40cb)

<div id="refer-anchor-12"></div>

- [12] [https://zhidao.baidu.com/question/471529802.html](https://zhidao.baidu.com/question/471529802.html)

<div id="refer-anchor-13"></div>

- [13] [https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/dd239408(v=sql.100)](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2008/dd239408(v=sql.100))

<div id="refer-anchor-14"></div>

- [14] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017)

<div id="refer-anchor-15"></div>

- [15] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017&viewFallbackFrom=sql-server-previousversions](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017&viewFallbackFrom=sql-server-previousversions)

<div id="refer-anchor-16"></div>

- [16] [https://zhidao.baidu.com/question/1640313408271084100.html](https://zhidao.baidu.com/question/1640313408271084100.html)

<div id="refer-anchor-17"></div>

- [17] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017)

<div id="refer-anchor-18"></div>

- [18] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/database-engine-configuration-account-provisioning?view=sql-server-2014](https://docs.microsoft.com/zh-cn/sql/sql-server/install/database-engine-configuration-account-provisioning?view=sql-server-2014)

<div id="refer-anchor-19"></div>

- [19] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server?view=sql-server-2017)

<div id="refer-anchor-20"></div>

- [20] [https://zhidao.baidu.com/question/177013795205167644.html](https://zhidao.baidu.com/question/177013795205167644.html)

<div id="refer-anchor-21"></div>

- [21] [https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017)

<div id="refer-anchor-22"></div>

- [22] [https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017)

<div id="refer-anchor-23"></div>

- [23] [https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017](https://docs.microsoft.com/zh-cn/sql/database-engine/configure-windows/server-configuration-options-sql-server?view=sql-server-2017)

<div id="refer-anchor-24"></div>

- [24] [https://docs.microsoft.com/zh-cn/dotnet/framework/data/adonet/sql/authentication-in-sql-server](https://docs.microsoft.com/zh-cn/dotnet/framework/data/adonet/sql/authentication-in-sql-server)

<div id="refer-anchor-25"></div>

- [25] [https://docs.microsoft.com/zh-cn/sql/sql-server/install/database-engine-configuration-account-provisioning?view=sql-server-2014](https://docs.microsoft.com/zh-cn/sql/sql-server/install/database-engine-configuration-account-provisioning?view=sql-server-2014)

<div id="refer-anchor-26"></div>

- [26] [https://blog.csdn.net/iamluole/article/details/9570833]https://blog.csdn.net/iamluole/article/details/9570833()

<div id="refer-anchor-27"></div>

- [27] [https://www.xuebuyuan.com/992629.html?mobile=1](https://www.xuebuyuan.com/992629.html?mobile=1)

<div id="refer-anchor-28"></div>

- [28] [https://blog.csdn.net/zw_2011/article/details/8872047](https://blog.csdn.net/zw_2011/article/details/8872047)

<div id="refer-anchor-29"></div>

- [29] [https://blog.csdn.net/randomparty/article/details/79477887](https://blog.csdn.net/randomparty/article/details/79477887)

<div id="refer-anchor-30"></div>

- [30] [https://blog.csdn.net/u011078141/article/details/89850434](https://blog.csdn.net/u011078141/article/details/89850434)

<div id="refer-anchor-31"></div>

- [31] [https://zhidao.baidu.com/question/490109816.html](https://zhidao.baidu.com/question/490109816.html)

<div id="refer-anchor-32"></div>