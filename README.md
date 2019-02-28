# system_language


其实一个操作系统，终究是在处理 数据 、运算 这两件事。  
数据 涉及到存储。按照数据存储距离CPU 的距离不同，划分成不同的存储。  

## CPU ---》 一级缓存  ---》二级缓存 ---》二级缓存 ---》 内存 ---》 硬盘（按照形式不同可以分为 SSD、机械硬盘）  

他们离CPU越来越远，存储容量原来越大，存储性价比越高，但是 对CPU就不友好了，CPU 读取数据的时间越来越长。  

人民研究各种算法，一是：找到规律，让CPU计算更快   二是：时空转换，找到 最好的性价比。（让人来觉得 时间、空间 两者之中找到平衡点。对于计算机本身来说，无好坏，它只是运行自然规律，来满足人类心理预期、需求而已。）  

C 语言可以写操作系统，就是他能更好的 操作 CPU、存储。  

其他语言 如果能过操作CPU、存储===》 其实也能写操作系统。  

前几周面试，让用PHP实现 order by 功能。  

我想这不是数据库的典型功能么？？？  

其实用PHP 也能实现MySQL。数据库这个产品，本身对外提供服务，有自己的协议。如果 你用PHP实现了一个数据，对外提供服务协议跟mysql的一样。你用PHP实现的数据库，也可以叫PHP,只是会有版权问题而已。  

为啥非得用PHP 在实现一遍呢。真无语。 但是这是面试。在这记录一下。  


参考
http://www.php.net/manual/zh/function.array-multisort.php
https://www.cnblogs.com/M-D-Luffy/p/4224127.html  


$data[] = array('volume' => 67, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 1);
$data[] = array('volume' => 85, 'edition' => 6);
$data[] = array('volume' => 98, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 6);
$data[] = array('volume' => 67, 'edition' => 7);

// 取得列的列表
foreach ($data as $key => $row) {
    $volume[$key]  = $row['volume'];
    $edition[$key] = $row['edition'];
}

// 将数据根据 volume 降序排列，根据 edition 升序排列
// 把 $data 作为最后一个参数，以通用键排序
array_multisort($volume, SORT_DESC, $edition, SORT_ASC, $data);


改进===》

$data[] = array('volume' => 67, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 1);
$data[] = array('volume' => 85, 'edition' => 6);
$data[] = array('volume' => 98, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 6);
$data[] = array('volume' => 67, 'edition' => 7);

$a = array_column($data, 'volume');

$b = array_column($data, 'edition');

$sort = array_multisort ($a, SORT_DESC,$b,SORT_DESC, $data);
var_dump($data);
die();


改进====》

$sort = array();
$sort = array(
    array('id'=>'desc'),
    array('name'=>'asc'),
    array('num'=>'desc'),
);

// 取得列的列表

// 取得列的列表
foreach ($sort as $key => $row) {
   foreach ($data as $key => $row) {
       $volume[$key]  = $row['volume'];
       $edition[$key] = $row['edition'];
}

$param = array();
froeach($sort as $value)
{
  $param[] = array_column($data, $value['key']);
  $param[] = $value['value'] ? $value['value'] : 'SORT_DESC' ;
}

$param[] = $data;

call_user_func_array('array_multisort', $param); 



气死我了。  
试了半天都失败了。fuck。什么鬼。call_user_func_array   array_column   array_multisort  
都什么鬼。。。。。。。不写了


