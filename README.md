# webfont

```
<?php
/** 字体映射关系   生成字体文件     比如 e1f2  真实代表的就是0   efab 代表的就是1
  这样也可能会有问题（因为我们只是加密0-9这十个数字，抓取数据对应规则很容易被人家猜出来）
  也可以 比如后端生成 rand（0,x） 个随机数 然后 取模生成  x 个 对应的字体文件 每一个 值对应一套 对应关系    让 e1f2 有的时候对应的是 数字1  有的时候对应的 数字2
  如果是ajax 请求 后端给前端 提供 相关数据（如果可以在做加密 （rsa 或者 自己写个公式 等等））
  当然这些不能完全挡住被人家抓取（再加入 ip  token  或者其他相关策略）
  ttf 转 svg  https://everythingfonts.com/ttf-to-svg
  svg 自定义 字体 映射规则  https://icomoon.io/app/#/select/font  这个站垃圾  ：  用这个 -> http://fontello.com/
 **/


function get_font_num($num)
{
    $result = '';

    $font_map = [
        0 => 'e1f2',
        1 => 'efab',
        2 => 'eba3',
        3 => 'ecfa',
        4 => 'edfd',
        5 => 'effa',
        6 => 'ef3a',
        7 => 'e6f5',
        8 => 'ecb2',
        9 => 'e8ae'
    ];

    for ($i = 0, $len = strlen($num); $i < $len; $i++) {
        $n = substr($num, $i, 1);
        if (is_numeric($n)) {
            $result .= '&#x' . $font_map[$n] . ';';
        } else {
            $result .= $n;
        }
    }

    return $result;
}

$data = [
    ['iphone1', 1321.9, 5],
    ['iphone2', 590.27, 5],
    ['iphone3', 389.76, 26],
    ['iphone4', 271.27, 1]
];

?>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html;charset=utf-8">
    <title></title>
    <style type="text/css">
        @font-face {
            font-family: 'my_webfont';
            src: url('fonts/icomoon.eot?fdipzone');
            src: url('fonts/icomoon.eot?fdipzone#iefix') format('embedded-opentype'),
            url('fonts/icomoon.ttf?fdipzone') format('truetype'),
            url('fonts/icomoon.woff?fdipzone') format('woff'),
            url('fonts/icomoon.svg?fdipzone#my_webfont') format('svg');
            font-weight: normal;
            font-style: normal;
        }
        .my_webfont {
            font-family: my_webfont !important;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            /**letter-spacing:-1px;*/
        }

        td {
            padding: 0px 5px 0px 5px;
            text-align: center;
        }

        .left {
            text-align: left;
        }

    </style>
</head>

<body>
<table>
    <tr>
        <td>排名</td>
        <td>手机</td>
        <td>金额</td>
        <td>数量</td>
    </tr>
    <?php
    for ($i = 0, $len = count($data); $i < $len; $i++) {
        echo '<tr>' . PHP_EOL;
        echo '<td>' . ($i + 1) . '</td>' . PHP_EOL;
        echo '<td class="left">' . $data[$i][0] . '</td>' . PHP_EOL;
        echo '<td class="my_webfont">' . get_font_num($data[$i][1]) . '</td>' . PHP_EOL;
        echo '<td class="my_webfont">' . get_font_num($data[$i][2]) . '台</td>' . PHP_EOL;
        echo '</tr>' . PHP_EOL;
    }
    ?>
</table>
</body>
</html>

```
