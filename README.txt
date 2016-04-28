# ResponsiveWeb
   这个项目是静态页面，是学习bootstrap实战这本书时，对照它的实战演练进行的。
   做这次网页包括了5个部分，包括主页：index.html;新闻页：index.html;小组页：team.html;打卡页：great.html;
和词根页：word.html。大概总共耗时3-4天的样子，其中出现了一些问题，但是也圆满解决，包括可能代码的书写不规范
导致样式上的不对;还有bootstrap里面专门的样式，比如只能<div class="container"></div>中包含<div class="row"></div>，
二者的顺序不能反之类的。总之收获还是蛮多的，学会了在bootstrap顶部导航固定，轮播图的效果，滚动监听等等。这里特别总
结出来3个印象比较深刻的点进行分析总结。
  
  第1点是今天才发现的，比较深刻，查阅了资料网站才解决，也不是什么大问题，但是也需要引起关注。
  问题是这样的，就是所有的网页当我在其他比如Chrome,Firefox,Opera,甚至是IE8+浏览器上，页面的样式都是非常好的，但是当我将其预览在360浏览器时，样式变得极其丑陋，全乱了套，作为开发者不能让用户去换浏览器，只能解决了。。
   查阅度娘后发现：360浏览器是这样的：对于此类浏览器，有时候号称双核或者N核的高速浏览器，其本质上就是本地IE浏览器的壳子，
外加Chrome抑或Firefox的内核，大部分情况下都是WebKit系列内核。
   而且是这样的：360,360极速(兼容模式),搜狗,qq浏览器--ie；谷歌,360极速(极速模式)--chrome，针对此问题度娘后发现有如下的解决
方式：
    content的取值为webkit,ie-comp,ie-stand之一，区分大小写，分别代表用webkit内核，IE兼容内核，IE标准内核。
	若页面需默认用极速核，增加标签：<meta name="renderer" content="webkit" charset="utf-8"> 
	若页面需默认用ie兼容内核，增加标签：<meta name="renderer" content="ie-comp" charset="utf-8"> 
	若页面需默认用ie标准内核，增加标签：<meta name="renderer" content="ie-stand" charset="utf-8">
	添加这些语句后，页面显示正常。
	此外还有一种方法，但是需要在用户使用前声明，即将极速模式切换为兼容模式，但是不太推荐，因为可能之后浏览网页的速度慢，降低用户体验。默认的话用户使用的360浏览器的极速模式的话，
	1、地址栏最后面有个“闪电”的图标，鼠标放上去会显示当前模式，
	2、点击一下，会显示两种模式，分别是“极速模式”和“兼容模式”。
    3、点击兼容模式后就是那个“闪电”图标变为“ie”图标了。
    对于极速模式和兼容模式，这里要说明一下：极速模式代表高速，速度快，浏览方便，而兼容模式即极力适合更多的浏览器，更多的考虑的是兼容。关于兼容模式，360的做法是保留了你电脑本身的IE内核，因为我电脑上装的是最新的IE10，所以当切换到兼容模式时，所有的网页就显示正常了。
      第2点是关于顶部固定导航条的使用吧，在news.html中这样写：
      <div class="container menu">
	    <ul class="nav nav-pills" id="menu">
	        <li><a href="#">首页</a> </li>
	        <li><a href="#">计划</a> </li>
	        <li><a href="#">最新报道</a> </li>
	        <li><a href="#">猜你喜欢</a> </li>
	        <li><a href="#">读过的文章</a> </li>
	    </ul>
      </div> 
      除了头部必要的这些书写：
    要想成功还需要2步，第一步：
    <script type="text/javascript">
        /*设置菜单当距离窗口顶部偏移距离小于86像素时，将激活附加导航插件*/
        $(function(){
            $("#menu").affix({
                offset:{top:86}
            })
        });
    </script>
    这里:Bootstrap附加导航（Affix）插件允许某个 <div> 固定在页面的某个位置。您也可以在打开或关闭使用该插件之间进行切换。
    第2步，有了第一步会发现在页面下拉时，顶部此固定导航栏会晃动，同时为了避免透明背景带来的上下文字重叠问题，定义宽度为100%;避免
 宽度固定后自动收缩。具体的style.css的样式如下：
		 #menu{
		    background: #E4E4E4;
		    width: 100%;
		    top:0;
            margin: 6px auto;
        }
		.menu .nav {
		    padding: 0;
		    margin: 0;
		}
		第3点总结的就是轮播的使用。轮播包含框需要指明ID值，carousel，slide类，框内包含3部分组件：标签框（carousel-indicators），图文内容框（carousel-inner）,左右导航框(carousel-control)。通过data-target="#carousel_box"属性启动轮播，使用data-slide-to="0"、data-slide="prev"、data-slide="next"定义交互按钮行为。
		<div id="carousel_box" class="carousel_slide">
			<ol class="carousel-indicators">
				<li data-target="#carousel_box" data-slide-to="0" class="active"></li>
				<li data-target="#carousel_box" data-slide-to="1"></li>
			</ol>
			<div class="carousel-inner">
               <div class="item active">
               	<a href="#"><img src="images/reader.jpg" alt="英语阅读" /> </a>
                 <div class="carousel-caption">
                     <div class="slide-col2">
                         <h2 style="padding: 10px;;">英语阅读</h2>
                         <div class="row">
                             <div class="span5" >
                                 <p>阅读，是比背诵更好的记忆；</p>
                                 <p>阅读，是检验词汇掌握程度的试金石；</p>
                                 <a class="more" href="#" target="_blank">了解英语阅读</a>
                                 <div class="span4" style="margin-left: 100%;margin-top:-12%"> <a class="btn btn-large btn-success" href="#">开始学习</a> </div>
                            </div>
                        </div>
                     </div>
                 </div>
               </div>
               <div class="item">
                 <a href="#"><img src="images/market.jpg" alt="Slide2"/> </a>
                 <div class="carousel-caption">
                     <div class="slide-col2">
                         <h2  style="padding: 10px;;">丰富的学习资料</h2>
                         <div class="row">
                             <div class="span5" >
                                 <h4>根据你的程度和目标，定制学习内容 </h4>
                                 <p>真人发音和中英文释义</p>
                             </div>
                             <div class="span4"><a class="btn btn-large btn-success" href="#" target="_blank">了解学习资料</a> </div>
                         </div>
                     </div>
                 </div>
             </div>
			</div>
			<a class="left carousel-control" href="#carousel_box" data-slide="prev">&lsaquo;</a>
			<a class="right carousel-control" href="#carousel_box" data-slide="next">&rsaquo;</a>
		</div>
		具体的css细节设置如下：
		#carousel_box{
           height: 770px;
         }
		.carousel-indicators{
		    top:530px;
		    left: 500px;
		}
		.carousel-caption{
		    top:540px;
		    background: #E4E4E4;
		}
		.carousel-inner{overflow: visible;}
		.carousel-caption h4,.carousel-caption p{line-height: 20px;color: #333;font-size: 18px;}
		.carousel-indicators li{background-color: #d4d5d6;}
		.carousel-indicators .active{background-color: #209e85;}
		.more{font-size: 16px;color: green;}

		以上就是这次的体会了。。
		                                                                                    写于2016.4.28
