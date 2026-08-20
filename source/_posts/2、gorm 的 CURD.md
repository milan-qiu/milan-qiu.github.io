---
title: "2、gorm 的 CURD"
date: "2022-01-09 22:05:00"
tags:
categories:
description: >-
  // Create db.Create(&table1{Name: "小明", Age: 80}) // INSERT INTO `table1` (`created_at`,`updated_at`,`deleted_at`,`name`,`age`) VALUES ('2022-01-09 22
---

<div class="cnblogs_code">
<pre><span style="color: #008000;">//</span><span style="color: #008000;"> Create</span>
db.Create(&amp;table1{Name: <span style="color: #800000;">"</span><span style="color: #800000;">小明</span><span style="color: #800000;">"</span>, Age: <span style="color: #800080;">80</span><span style="color: #000000;">}) 
</span><span style="color: #008000;">//</span><span style="color: #008000;"> INSERT INTO `table1` (`created_at`,`updated_at`,`deleted_at`,`name`,`age`) VALUES ('2022-01-09 22:01:03.982','2022-01-09 22:01:03.982',NULL,'小明',80)

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Read</span>
<span style="color: #0000ff;">var</span><span style="color: #000000;"> person table1
db.First(</span>&amp;person, <span style="color: #800080;">1</span>) <span style="color: #008000;">//</span><span style="color: #008000;"> 根据整形主键查找 
</span><span style="color: #008000;">//</span><span style="color: #008000;"> SELECT * FROM `table1` WHERE `table1`.`id` = 1 AND `table1`.`deleted_at` IS NULL ORDER BY `table1`.`id` LIMIT 1</span>
db.First(&amp;person, <span style="color: #800000;">"</span><span style="color: #800000;">name = ?</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">小明</span><span style="color: #800000;">"</span><span style="color: #000000;">) 
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 查找 name 字段值为 小明 的记录 </span><span style="color: #008000;">//</span><span style="color: #008000;"> SELECT * FROM `table1` WHERE name = '小明' AND `table1`.`deleted_at` IS NULL ORDER BY `table1`.`id` LIMIT 1

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Update - 将 person 的 Name 更新为 小东</span>
db.Model(&amp;person).Update(<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">小东</span><span style="color: #800000;">"</span><span style="color: #000000;">) 
</span><span style="color: #008000;">//</span><span style="color: #008000;">UPDATE `table1` SET `name`='小东',`updated_at`='2022-01-09 21:57:35.378'

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Update - 更新多个字段</span>
db.Model(&amp;person).Updates(table1{Name: <span style="color: #800000;">"</span><span style="color: #800000;">小明</span><span style="color: #800000;">"</span>, Age: <span style="color: #800080;">80</span>}) <span style="color: #008000;">//</span><span style="color: #008000;"> 仅更新非零值字段 
</span><span style="color: #008000;">//</span><span style="color: #008000;">UPDATE `table1` SET `updated_at`='2022-01-09 21:59:08.109',`name`='小明',`age`=80</span>
db.Model(&amp;person).Updates(map[<span style="color: #0000ff;">string</span>]<span style="color: #0000ff;">interface</span>{}{<span style="color: #800000;">"</span><span style="color: #800000;">Name</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">小明一号</span><span style="color: #800000;">"</span>, <span style="color: #800000;">"</span><span style="color: #800000;">Age</span><span style="color: #800000;">"</span>: <span style="color: #800080;">80</span><span style="color: #000000;">}) 
</span><span style="color: #008000;">//</span><span style="color: #008000;">UPDATE `table1` SET `age`=80,`name`='小明一号',`updated_at`='2022-01-09 21:59:52.966'

</span><span style="color: #008000;">//</span><span style="color: #008000;"> Delete - 删除 person</span>
db.Delete(&amp;person, <span style="color: #800080;">1</span><span style="color: #000000;">) 
</span><span style="color: #008000;">//</span><span style="color: #008000;">UPDATE `table1` SET `deleted_at`='2022-01-09 22:00:32.07' WHERE `table1`.`id` = 1 AND `table1`.`deleted_at` IS NULL<br /></span></pre>
</div>
<p>&nbsp;</p>
