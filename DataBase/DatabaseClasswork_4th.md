# 数据库第4次随堂作业

<center>PHP数据库编程</center>



> written by panzy25, 18372046
>
> Typora used
>
> Based on Markdown

[TOC]

## 1. Overview

1. php-odbc 编程访问并显示“学生”这个表
2. php-sqlsrv 编程访问并显示“学生”这个表
3. 处理数据库密码错误和 Select 语句错误

## 2. php-odbc 编程访问并显示“学生”这个表

```php
<?php
$server='222.200.184.125'; $database='cap1'; $user='zixun18'; $pass='zixun@18';
echo "<br />";
// 连接数据库 $connection=odbc_connect("Driver={SQL 10.0};Server=$server;Database=$database;",$user,$pass);
if (!$connection)
{exit("Connection Failed: " . $connection);}
Native
Client
// 进行学生表查询
$sql="SELECT * FROM 学生"; $rs=odbc_exec($connection,$sql); if (!$rs)
{exit("Error in SQL");}
// 利用游标获取数据
// 显示表头
echo "<table border='3' valign='middle'>学生<tr>"; echo "<th>学号</th>";
echo "<th>姓名</th>";
echo "<th>性别</th>";
echo "<th>专业</th>";
echo "<th>出生日期</th></tr>";
Server
// 逐行获取并显示
while (odbc_fetch_row($rs)) {
$sid=odbc_result($rs,"学号"); $sname=odbc_result($rs,"姓名"); $sex=odbc_result($rs,"性别"); $smaj=odbc_result($rs,"专业"); $sbirth=odbc_result($rs,"出生日期");
echo "<tr><td>$sid</td>"; echo "<td>$sname</td>"; echo "<td>$sex</td>";
echo "<td>$smaj</td>";
echo "<td>$sbirth</td></tr>";
}
odbc_close($connection); // 关闭数据库连接 ?>
```

## 3. php-sqlsrv 编程访问并显示“学生”这个表

```php
<?php
$serverName = "222.200.184.125\sqlexpress"; //serverName\instanceName
$connectionInfo = array( "Database"=>"cap1", "UID"=>"zixun18", "PWD"=>"zixun@18"); @$conn = sqlsrv_connect( $serverName, $connectionInfo);
if( $conn ) {
echo "Connection by Sqlsrv_connet successfully.<br />"; echo "<br />";
}else{
echo "Connection could not be established.<br />"; die( print_r( sqlsrv_errors(), true));
}
$sql="SELECT * FROM 学生"; //$params = array(); @$rs=sqlsrv_query($conn,$sql);
if (!$rs)
{exit("Error in SQL");}
echo "<table border='3' valign='middle'>学生<tr>"; echo "<th>学号</th>";
echo "<th>姓名</th>";
echo "<th>性别</th>";
echo "<th>专业</th>";
echo "<th>出生日期</th></tr>";
while (sqlsrv_fetch($rs)!=null) {
$sid =sqlsrv_get_field($rs,0); $sname =sqlsrv_get_field($rs,1); $sex =sqlsrv_get_field($rs,2); $smaj =sqlsrv_get_field($rs,3); $sbirth =sqlsrv_get_field($rs,4);
echo "<tr><td>$sid</td>"; echo "<td>$sname</td>"; echo "<td>$sex</td>";
echo "<td>$smaj</td>";
echo "<td>$sbirth</td></tr>";
}
echo "<br />"; sqlsrv_close( $conn ); echo "<br />";
?>
```

## 4. 处理数据库密码错误和 Select 语句错误

```php
@$connection=odbc_connect(“Driver=(SQL Server Native Client 10.0);
                        Server=$server;Database=$database;”,$user,$pass);
// 需要紧跟错误处理 if (odbc_error()) {
echo odbc_errormsg();
exit(“Connection Failed-ODBC:” . $connection);
// PHP 正常退出，数据库返回出错;若是 PHP 出错，返回 500，内部服务器错误
}
if (!$connection) {
exit(“Connection Failed:” . $connection); }

$sql=”SELECT * FROM customers”; 
$rs=odbc_exec($connection, $sql); // 忽略执行错误 if (!$rs)
{exit(“Error in SQL”);}
```