# ie8hack
ie8下的兼容问题处理：背景透明，css3圆角，css3和jquery支持部分css3选择器（例如：nth-child）,支持html5的语义化标签，媒体查询@media等。

###在html页面头部<head>优先加载ie8需要的插件，因为部分插件需要依赖jquery,所以jquery需要最先加载。
*样式css：如果是其他的样式.css就添加在<head>里面的全局global.css后面*

    <head>
    <meta charset="UTF-8">
    <title>车险保费计算</title>
    <script src="../../../public/js/jquery-1.11.2.min.js"></script>
    <!--[if lte IE 8]>
    <script type="text/javascript" src="../../../public/js/html5.js"></script>
    <script type="text/javascript" src="../../../public/js/respond.min.js"></script>
    <script type="text/javascript" src="../../../public/js/selectivizr-min.js"></script>
    <![endif]-->

    <!--[if IE 6]>
    <script type="text/javascript" src="../../../public/js/DD_belatedPNG_0.0.8a.min.js"></script>
    <script>
        DD_belatedPNG.fix('*');
    </script>
    <![endif]-->

    <!--全局css-->
    <link rel="stylesheet" type="text/css" href="../../../public/css/global.css"/>
    </head>
* * * *
*脚本js：如果是其他的插件和逻辑js就添加在 </body>的上方。注意顺序，插件js优先添加。*

    <script src="../../../public/js/jquery.easydropdown.js"></script>
    <!--全局js-->
    <script src="../../../public/js/global.js"></script>
    <!--逻辑js-->
    <script src="../js/calcPrice.js"></script>
    </body>
    </html>
* * * *
