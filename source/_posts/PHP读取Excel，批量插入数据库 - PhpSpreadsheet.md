---
title: "PHP读取Excel，批量插入数据库 - PhpSpreadsheet"
date: "2020-06-17 14:41:00"
updated: "2020-06-28 22:12:00"
tags:
categories:
description: >-
  PhpSpreadsheet [ˈspredʃiːt] 准备 一、利用composer安装PhpSpreadsheet到项目目录 composer require phpoffice/phpspreadsheet 二、新建public目录，并进入新建test.php 三、在项目根目录新建conn.p
---

<h2 class="_1RuRku">PhpSpreadsheet&nbsp;&nbsp;&nbsp;[ˈspredʃiːt]</h2>
<h3>准备</h3>
<p>一、利用composer安装PhpSpreadsheet到项目目录</p>
<div class="cnblogs_code">
<pre>composer require phpoffice/phpspreadsheet</pre>
</div>
<p>二、新建public目录，并进入新建test.php</p>
<p>三、在项目根目录新建conn.php，并往里面填写数据库信息</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
$servername </span>= <span style="color: #800000;">"</span><span style="color: #800000;">localhost</span><span style="color: #800000;">"</span><span style="color: #000000;">;
$username </span>= <span style="color: #800000;">"</span><span style="color: #800000;">root</span><span style="color: #800000;">"</span><span style="color: #000000;">;
$password </span>= <span style="color: #800000;">"</span><span style="color: #800000;">root</span><span style="color: #800000;">"</span><span style="color: #000000;">;
$dbname </span>= <span style="color: #800000;">"</span><span style="color: #800000;">tt</span><span style="color: #800000;">"</span><span style="color: #000000;">;
 
</span><span style="color: #008000;">//</span><span style="color: #008000;"> 创建连接</span>
$conn = <span style="color: #0000ff;">new</span><span style="color: #000000;"> mysqli($servername, $username, $password, $dbname);
</span><span style="color: #008000;">//</span><span style="color: #008000;"> Check connection</span>
<span style="color: #0000ff;">if</span> ($conn-&gt;<span style="color: #000000;">connect_error) {
    die(</span><span style="color: #800000;">"</span><span style="color: #800000;">连接失败: </span><span style="color: #800000;">"</span> . $conn-&gt;<span style="color: #000000;">connect_error);
} 
</span>?&gt;</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>生成.xlsx文件，并往里面填入信息</h3>
<p>test.php里面写</p>
<div class="cnblogs_code">
<pre>&lt;?<span style="color: #000000;">php
    require </span><span style="color: #800000;">'</span><span style="color: #800000;">../vendor/autoload.php</span><span style="color: #800000;">'</span><span style="color: #000000;">;
    
    use PhpOffice\PhpSpreadsheet\Spreadsheet;
    use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
    
    $spreadsheet </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Spreadsheet();
    $sheet </span>= $spreadsheet-&gt;<span style="color: #000000;">getActiveSheet();
    $sheet</span>-&gt;setCellValue(<span style="color: #800000;">'</span><span style="color: #800000;">A1</span><span style="color: #800000;">'</span>, <span style="color: #800000;">'</span><span style="color: #800000;">Welcome to Helloweba.</span><span style="color: #800000;">'</span>);<span style="color: #008000;">//</span><span style="color: #008000;">将信息填入A1单元格</span>
<span style="color: #000000;">    
    $writer </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Xlsx($spreadsheet);
    $writer</span>-&gt;save(<span style="color: #800000;">'</span><span style="color: #800000;">hello.xlsx</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">保存为hello.xlsx</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>将Excel的数据批量导入Mysql</h3>
<div class="cnblogs_code">
<pre>require <span style="color: #800000;">'</span><span style="color: #800000;">vendor/autoload.php</span><span style="color: #800000;">'</span><span style="color: #000000;">;

include(</span><span style="color: #800000;">'</span><span style="color: #800000;">conn.php</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">连接数据库</span>
<span style="color: #000000;">
$reader </span>= \PhpOffice\PhpSpreadsheet\IOFactory::createReader(<span style="color: #800000;">'</span><span style="color: #800000;">Xlsx</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$reader</span>-&gt;<span style="color: #000000;">setReadDataOnly(TRUE);
$spreadsheet </span>= $reader-&gt;load(<span style="color: #800000;">'</span><span style="color: #800000;">students.xlsx</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">载入excel表格</span>
<span style="color: #000000;">
$worksheet </span>= $spreadsheet-&gt;<span style="color: #000000;">getActiveSheet();
$highestRow </span>= $worksheet-&gt;getHighestRow(); <span style="color: #008000;">//</span><span style="color: #008000;"> 总行数</span>
$highestColumn = $worksheet-&gt;getHighestColumn(); <span style="color: #008000;">//</span><span style="color: #008000;"> 总列数</span>
$highestColumnIndex = \PhpOffice\PhpSpreadsheet\Cell\Coordinate::columnIndexFromString($highestColumn); <span style="color: #008000;">//</span><span style="color: #008000;"> e.g. 5</span>
<span style="color: #000000;">
$lines </span>= $highestRow - <span style="color: #800080;">2</span><span style="color: #000000;">; 
</span><span style="color: #0000ff;">if</span> ($lines &lt;= <span style="color: #800080;">0</span><span style="color: #000000;">) {
    exit(</span><span style="color: #800000;">'</span><span style="color: #800000;">Excel表格中没有数据</span><span style="color: #800000;">'</span><span style="color: #000000;">);
}

$sql </span>= <span style="color: #800000;">"</span><span style="color: #800000;">INSERT INTO `t_student` (`name`, `chinese`, `maths`, `english`) VALUES </span><span style="color: #800000;">"</span><span style="color: #000000;">;

</span><span style="color: #0000ff;">for</span> ($row = <span style="color: #800080;">3</span>; $row &lt;= $highestRow; ++<span style="color: #000000;">$row) {
    $name </span>= $worksheet-&gt;getCellByColumnAndRow(<span style="color: #800080;">1</span>, $row)-&gt;getValue(); <span style="color: #008000;">//</span><span style="color: #008000;">姓名</span>
    $chinese = $worksheet-&gt;getCellByColumnAndRow(<span style="color: #800080;">2</span>, $row)-&gt;getValue(); <span style="color: #008000;">//</span><span style="color: #008000;">语文</span>
    $maths = $worksheet-&gt;getCellByColumnAndRow(<span style="color: #800080;">3</span>, $row)-&gt;getValue(); <span style="color: #008000;">//</span><span style="color: #008000;">数学</span>
    $english = $worksheet-&gt;getCellByColumnAndRow(<span style="color: #800080;">4</span>, $row)-&gt;getValue(); <span style="color: #008000;">//</span><span style="color: #008000;">外语</span>
<span style="color: #000000;">
    $sql .</span>= <span style="color: #800000;">"</span><span style="color: #800000;">('$name','$chinese','$maths','$english'),</span><span style="color: #800000;">"</span><span style="color: #000000;">;
}
$sql </span>= rtrim($sql, <span style="color: #800000;">"</span><span style="color: #800000;">,</span><span style="color: #800000;">"</span>); <span style="color: #008000;">//</span><span style="color: #008000;">去掉最后一个,号</span>
<span style="color: #0000ff;">try</span><span style="color: #000000;"> {
    $db</span>-&gt;<span style="color: #000000;">query($sql);
    echo </span><span style="color: #800000;">'</span><span style="color: #800000;">OK</span><span style="color: #800000;">'</span><span style="color: #000000;">;
} </span><span style="color: #0000ff;">catch</span><span style="color: #000000;"> (Exception $e) {
    echo $e</span>-&gt;<span style="color: #000000;">getMessage();
}</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Mysql批量导出数据到Excel</h3>
<p>一、设置表头</p>
<div class="cnblogs_code">
<pre>require <span style="color: #800000;">'</span><span style="color: #800000;">vendor/autoload.php</span><span style="color: #800000;">'</span><span style="color: #000000;">;

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

include(</span><span style="color: #800000;">'</span><span style="color: #800000;">conn.php</span><span style="color: #800000;">'</span>); <span style="color: #008000;">//</span><span style="color: #008000;">连接数据库</span>
<span style="color: #000000;">
$spreadsheet </span>= <span style="color: #0000ff;">new</span><span style="color: #000000;"> Spreadsheet();
$worksheet </span>= $spreadsheet-&gt;<span style="color: #000000;">getActiveSheet();
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置工作表标题名称</span>
$worksheet-&gt;setTitle(<span style="color: #800000;">'</span><span style="color: #800000;">学生成绩表</span><span style="color: #800000;">'</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">表头
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置单元格内容</span>
$worksheet-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">1</span>, <span style="color: #800080;">1</span>, <span style="color: #800000;">'</span><span style="color: #800000;">学生成绩表</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">1</span>, <span style="color: #800080;">2</span>, <span style="color: #800000;">'</span><span style="color: #800000;">姓名</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">2</span>, <span style="color: #800080;">2</span>, <span style="color: #800000;">'</span><span style="color: #800000;">语文</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">3</span>, <span style="color: #800080;">2</span>, <span style="color: #800000;">'</span><span style="color: #800000;">数学</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">4</span>, <span style="color: #800080;">2</span>, <span style="color: #800000;">'</span><span style="color: #800000;">外语</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">5</span>, <span style="color: #800080;">2</span>, <span style="color: #800000;">'</span><span style="color: #800000;">总分</span><span style="color: #800000;">'</span><span style="color: #000000;">);

</span><span style="color: #008000;">//</span><span style="color: #008000;">合并单元格</span>
$worksheet-&gt;mergeCells(<span style="color: #800000;">'</span><span style="color: #800000;">A1:E1</span><span style="color: #800000;">'</span><span style="color: #000000;">);

$styleArray </span>=<span style="color: #000000;"> [
    </span><span style="color: #800000;">'</span><span style="color: #800000;">font</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
        </span><span style="color: #800000;">'</span><span style="color: #800000;">bold</span><span style="color: #800000;">'</span> =&gt; <span style="color: #0000ff;">true</span><span style="color: #000000;">
    ],
    </span><span style="color: #800000;">'</span><span style="color: #800000;">alignment</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
        </span><span style="color: #800000;">'</span><span style="color: #800000;">horizontal</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> \PhpOffice\PhpSpreadsheet\Style\Alignment::HORIZONTAL_CENTER,
    ],
];
</span><span style="color: #008000;">//</span><span style="color: #008000;">设置单元格样式</span>
$worksheet-&gt;getStyle(<span style="color: #800000;">'</span><span style="color: #800000;">A1</span><span style="color: #800000;">'</span>)-&gt;applyFromArray($styleArray)-&gt;getFont()-&gt;setSize(<span style="color: #800080;">28</span><span style="color: #000000;">);

$worksheet</span>-&gt;getStyle(<span style="color: #800000;">'</span><span style="color: #800000;">A2:E2</span><span style="color: #800000;">'</span>)-&gt;applyFromArray($styleArray)-&gt;getFont()-&gt;setSize(<span style="color: #800080;">14</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>二、读取数据</p>
<div class="cnblogs_code">
<pre>$sql = <span style="color: #800000;">"</span><span style="color: #800000;">SELECT id,name,chinese,maths,english FROM `t_student`</span><span style="color: #800000;">"</span><span style="color: #000000;">;
$stmt </span>= $db-&gt;<span style="color: #000000;">query($sql);
$rows </span>= $stmt-&gt;<span style="color: #000000;">fetchAll(PDO::FETCH_ASSOC);
$len </span>=<span style="color: #000000;"> count($rows);
$j </span>= <span style="color: #800080;">0</span><span style="color: #000000;">;
</span><span style="color: #0000ff;">for</span> ($i=<span style="color: #800080;">0</span>; $i &lt; $len; $i++<span style="color: #000000;">) { 
    $j </span>= $i + <span style="color: #800080;">3</span>; <span style="color: #008000;">//</span><span style="color: #008000;">从表格第3行开始</span>
    $worksheet-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">1</span>, $j, $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">name</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
    $worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">2</span>, $j, $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">chinese</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
    $worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">3</span>, $j, $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">maths</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
    $worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">4</span>, $j, $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">english</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
    $worksheet</span>-&gt;setCellValueByColumnAndRow(<span style="color: #800080;">5</span>, $j, $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">chinese</span><span style="color: #800000;">'</span>] + $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">maths</span><span style="color: #800000;">'</span>] + $rows[$i][<span style="color: #800000;">'</span><span style="color: #800000;">english</span><span style="color: #800000;">'</span><span style="color: #000000;">]);
}

$styleArrayBody </span>=<span style="color: #000000;"> [
    </span><span style="color: #800000;">'</span><span style="color: #800000;">borders</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
        </span><span style="color: #800000;">'</span><span style="color: #800000;">allBorders</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
            </span><span style="color: #800000;">'</span><span style="color: #800000;">borderStyle</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> \PhpOffice\PhpSpreadsheet\Style\Border::BORDER_THIN,
            </span><span style="color: #800000;">'</span><span style="color: #800000;">color</span><span style="color: #800000;">'</span> =&gt; [<span style="color: #800000;">'</span><span style="color: #800000;">argb</span><span style="color: #800000;">'</span> =&gt; <span style="color: #800000;">'</span><span style="color: #800000;">666666</span><span style="color: #800000;">'</span><span style="color: #000000;">],
        ],
    ],
    </span><span style="color: #800000;">'</span><span style="color: #800000;">alignment</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> [
        </span><span style="color: #800000;">'</span><span style="color: #800000;">horizontal</span><span style="color: #800000;">'</span> =&gt;<span style="color: #000000;"> \PhpOffice\PhpSpreadsheet\Style\Alignment::HORIZONTAL_CENTER,
    ],
];
$total_rows </span>= $len + <span style="color: #800080;">2</span><span style="color: #000000;">;
</span><span style="color: #008000;">//</span><span style="color: #008000;">添加所有边框/居中</span>
$worksheet-&gt;getStyle(<span style="color: #800000;">'</span><span style="color: #800000;">A1:E</span><span style="color: #800000;">'</span>.$total_rows)-&gt;applyFromArray($styleArrayBody);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>三、下载保存为 .xlsx 文件</p>
<div class="cnblogs_code">
<pre>$filename = <span style="color: #800000;">'</span><span style="color: #800000;">成绩表.xlsx</span><span style="color: #800000;">'</span><span style="color: #000000;">;
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</span><span style="color: #800000;">'</span><span style="color: #000000;">);
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Content-Disposition: attachment;filename="</span><span style="color: #800000;">'</span>.$filename.<span style="color: #800000;">'</span><span style="color: #800000;">"</span><span style="color: #800000;">'</span><span style="color: #000000;">);
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Cache-Control: max-age=0</span><span style="color: #800000;">'</span><span style="color: #000000;">);

$writer </span>= \PhpOffice\PhpSpreadsheet\IOFactory::createWriter($spreadsheet, <span style="color: #800000;">'</span><span style="color: #800000;">Xlsx</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$writer</span>-&gt;save(<span style="color: #800000;">'</span><span style="color: #800000;">php://output</span><span style="color: #800000;">'</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>四、下载保存为 .xls 文件</p>
<div class="cnblogs_code">
<pre>$filename = <span style="color: #800000;">'</span><span style="color: #800000;">成绩表.xlsx</span><span style="color: #800000;">'</span><span style="color: #000000;">;
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Content-Type: application/vnd.ms-excel</span><span style="color: #800000;">'</span><span style="color: #000000;">);
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Content-Disposition: attachment;filename="</span><span style="color: #800000;">'</span>.$filename.<span style="color: #800000;">'</span><span style="color: #800000;">"</span><span style="color: #800000;">'</span><span style="color: #000000;">);
header(</span><span style="color: #800000;">'</span><span style="color: #800000;">Cache-Control: max-age=0</span><span style="color: #800000;">'</span><span style="color: #000000;">);

$writer </span>= \PhpOffice\PhpSpreadsheet\IOFactory::createWriter($spreadsheet, <span style="color: #800000;">'</span><span style="color: #800000;">xls</span><span style="color: #800000;">'</span><span style="color: #000000;">);
$writer</span>-&gt;save(<span style="color: #800000;">'</span><span style="color: #800000;">php://output</span><span style="color: #800000;">'</span>);</pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>其他操作</h3>
<p><a href="https://www.jianshu.com/p/10e1f047f2bd">https://www.jianshu.com/p/10e1f047f2bd</a></p>
