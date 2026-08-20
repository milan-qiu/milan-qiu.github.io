---
title: "ThinkPHP 5 配置方式"
date: "2020-03-29 09:32:00"
tags:
categories:
description: >-
  一、Model 1、在application下，新建 common\model 文件夹，在model文件夹里面新建 TableName.php（TableName为表名） 2、在TableName.php里面写： <?phpnamespace app\common\model;use think\M
---

<p><strong>一、Model</strong></p>
<p>1、在application下，新建 common\model 文件夹，在model文件夹里面新建&nbsp; TableName.php（TableName为表名）</p>
<p>2、在TableName.php里面写：</p>
<p>&lt;?php<br />namespace app\common\model;<br />use think\Model;</p>
<p>class Teacher extends Model<br />{</p>
<p>}</p>
<p>3、在application下的database.php设置数据库的相关信息</p>
<p>&nbsp;</p>
<p><strong>二、View</strong></p>
<p>1、在 application\index 下，新建view文件夹</p>
<p>2、在view文件夹里面新建 ControllerName 文件夹（ControllerName为控制器名）</p>
<p>3、把视图文件放到ControllerName里面</p>
<p>&nbsp;</p>
<p><strong>三、Control</strong></p>
<p>1、在application\config.php中，打开调试模式，app_debug改为true ；打开控制器类后缀，controller_suffix改为true</p>
<p>2、在application\index\controller 的Index.php，重命名为IndexController.php</p>
<p>3、在namespace下面引入内置的控制器，use think\Controller;</p>
<p>4、class Index改成：class IndexController extends Controller</p>
<p>&nbsp;</p>
<p><strong>四、Other</strong></p>
<p>1、css、js、img等文件夹直接放在public下面</p>
<p>2、&rdquo;/&rdquo;目录为public</p>
