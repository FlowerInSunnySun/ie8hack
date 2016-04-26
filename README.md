# ie8hack
ie8下的兼容问题处理：背景透明，css3圆角，css3和jquery支持部分css3选择器（例如：nth-child）,支持html5的语义化标签，媒体查询@media等。
### 在html页面头部<head>优先加载ie8需要的插件，因为部分插件需要依赖jquery,所以jquery需要最先加载。然后用IE的条件注释添加需要的脚本

> ####样式css：如果是其他的样式.css就添加在<head>里面的全局global.css后面 


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





> ####脚本js：如果是其他的插件和逻辑js就添加在 </body>的上方。注意顺序，插件js优先添加。

    <script src="../../../public/js/jquery.easydropdown.js"></script>
    <!--全局js-->
    <script src="../../../public/js/global.js"></script>
    <!--逻辑js-->
    <script src="../js/calcPrice.js"></script>
    </body>
    </html>

###css细节注意点
> 只要如上添加插件js就可以在ie8下使用css3和jquery css3选择器**nth-child**,html5语义化标签，如：section articel，媒体查询**@media**等。



> 圆角border-radius

![图片描述][1]





![图片描述][2]




  [1]: /img/bVvbnk
  [2]: /img/bVvbol

####兼容ie8css3圆角的PIE.htc文件的使用方法：

 - 直接将pie.htc文件放在项目结构里，如图1的红色块1
 - 如图1的**红色块2 calcPrice.html**添加的样式如图1的红色块3**calcPrice.css**里面的样式用到圆角，需在后面添加**behavior: url(../../../public/css/PIE.htc)**;
 - 关键来了，behavior后面的url路径不是css相对pie，这个和我们平时的background-image使用不一样。这个路径是html相对的pie路径。你也可以理解成calcPrice.html这个页面添加图1红色块1上面的global.css 的路径就是behavior: url(../../../public/css/PIE.htc)的正确路径了，因为pie文件和global.css 文件在同一个目录下。


> ie8背景透明opacity
- 在ie8下背景透明opacity=0而透明层上没文字或图片内容的时候，可以在opacity=20;下一行直接添加 filter:Alpha(opacity=20);

- 但是透明的背景上有内容的时候，在ie8只像上面加了filter:Alpha，是不是觉得就像你大冬天在浴室带着眼镜洗热水澡看到的情景。。。。。眼前一片朦胧~~~
    
      假设我们需要设置下面的div背景透明而文字不透明
      <div class=" coverModal">        <!--用于定位 -->
        <div class="coverBg ">        <!--背景透明的块 -->
          <div class="coverCon">我是文字，我不想被透明啊~</div>   <!--主体内容 -->
          </div> 
      </div> 
    


----------


    /*遮盖层公共样式*/
        .coverModal{
        display: none;
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        margin-left: -6%;
        z-index: 9999;
   }
    .coverBg {
        height:100%;
        background-color: rgba(0,0,0,0.5);
        /* IE9、标准浏览器、IE6和部分IE7内核的浏览器(如QQ浏览器)会读懂 */
    }
  
    .coverBg .coverCon{
        color: #FFFFFF;
    }
    @media \0screen\,screen\9 {
        /* 只支持IE6、7、8 */
        .coverBg {
            background-color:#000000;
            filter:Alpha(opacity=20);
            position:static; 
            /* IE6、7、8只能设置position:static(默认属性) ，否则会导致子元素继承Alpha值 */
            *zoom:1; 
            /* 激活IE6、7的haslayout属性，让它读懂Alpha */
        }
        .coverBg .coverCon{
            position: relative;
            /* 设置子元素为相对定位，可让子元素不继承Alpha值 */
        }
    }    
    


> 其他的hack

    background-color:red;
    background-color:red\0;  /* ie 8/9*/
    background-color:blue\9\0;  /* ie 9*/
    
    /*ie11 css hack*/ 
    @media all and (-ms-high-contrast:none) { 
    *::-ms-backdrop, .class名字 { 里面的样式:样式值;} 
    } 
    
    /*ie10 css hack*/ 
    @media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) { 
    .class名字 { 里面的样式:样式值;} 
    }
      
    
