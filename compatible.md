# 浏览器常见的兼容问题

## css

-  padding和margin

        padding：0；margin：0；

-  块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大

        在float的标签样式控制中加入 display:inline;将其转化为行内属性

-  设置较小高度标签（一般小于10px），在ie6，ie7，遨游中高度超出自己设置高度

        给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。

-  行内属性标签，设置display:block后采用float布局，又有横行的margin的情况，ie6间距bug

        在display:block;后面加入display:inline;display:table;

-  图片默认有间距

        使用float属性为img布局（因为img标签是行内属性标签，所以只要不超出容器宽度，img标签都会排在一行里，但是部分浏览器的img标签之间会有个间距。去掉这个间距使用float是正道）

-  标签最低高度设置min-height不兼容

        如果我们要设置一个标签的最小高度200px，需要进行的设置为：{min-height:200px; height:auto !important; height:200px; overflow:visible;}

-  元素水平居中问题

        FF: margin:0 auto;
        IE: 父级{ text-align:center; }

-  Div的垂直居中问题

        vertical-align:middle; 将行距增加到和整个DIV一样高：line-height:200px; 然后插入文字，就垂直居中了。缺点是要控制内容不要换行。

-  float的div闭合;清除浮动;自适应高度

        ① 例如：＜div id=”floatA” >＜div id=”floatB” >＜div id=”NOTfloatC” >
        这里的NOTfloatC并不希望继续平移，而是希望往下排。(其中floatA、floatB的属性已经设置为float:left;)
        这段代码在IE中毫无问题，问题出在FF。原因是NOTfloatC并非float标签，必须将float标签闭合。在 ＜div class=”floatB”> ＜div class=”NOTfloatC”>之间加上 ＜div class=”clear”>这个div一定要注意位置，而且必须与两个具有float属性的div同级，之间不能存在嵌套关系，否则会产生异常。并且将clear这种样式定义为为如下即可： .clear{ clear:both;}
        ② 作为外部 wrapper 的 div 不要定死高度,为了让高度能自适应，要在wrapper里面加上overflow:hidden; 当包含float的box的时候，高度自适应在IE下无效，这时候应该触发IE的layout私有属性(万恶的IE啊！)用zoom:1;可以做到，这样就达到了兼容。
        例如某一个wrapper如下定义：
        .colwrapper{ overflow:hidden; zoom:1; margin:5px auto;}
        ③ 对于排版,我们用得最多的css描述可能就是float:left.有的时候我们需要在n栏的float div后面做一个统一的背景,譬如:
        <div id=”page”>
        <div id=”left”>＜/div>
        <div id=”center”>＜/div>
        <div id=”right”>＜/div>
        </div>
        比如我们要将page的背景设置成蓝色,以达到所有三栏的背景颜色是蓝色的目的,但是我们会发现随着left center right的向下拉长,而page居然保存高度不变,问题来了,原因在于page不是float属性,而我们的page由于要居中,不能设置成float,所以我们应该这样解决：
        <div id=”page”>
        <div id=”bg” style=”float:left;width:100%”>
        <div id=”left”>＜/div>
        <div id=”center”>＜/div>
        <div id=”right”>＜/div>
        </div>
        </div>
        再嵌入一个float left而宽度是100%的DIV解决之。
        ④ 万能float 闭合(非常重要!)
        关于 clear float 的原理可参见 [How To Clear Floats Without Structural Markup],将以下代码加入Global CSS 中,给需要闭合的div加上class="clearfix" 即可,屡试不爽。
        /* Clear Fix */
        .clearfix:after { content:"."; display:block; height:0; clear:both; visibility:hidden; }
        .clearfix { display:inline-block; }
        /* Hide from IE Mac */
        .clearfix {display:block;}
        /* End hide from IE Mac */
        /* end of clearfix */
        或者这样设置：.hackbox{ display:table; //将对象作为块元素级的表格显示}


-  LI中内容超过长度后以省略号显示

        此技巧适用与IE、Opera、safari、chrom浏览器，FF暂不支持。
        <style type="text/css">
        <!--
        li {
        width:200px;
        white-space:nowrap;
        text-overflow:ellipsis;
        -o-text-overflow:ellipsis;
        overflow: hidden;
        }
        -->
        </style>

-  为什么web标准中IE无法设置滚动条颜色了

        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
        <meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
        <style type="text/css">
        <!--
        html {
        scrollbar-face-color:#f6f6f6;
        scrollbar-highlight-color:#fff;
        scrollbar-shadow-color:#eeeeee;
        scrollbar-3dlight-color:#eeeeee;
        scrollbar-arrow-color:#000;
        scrollbar-track-color:#fff;
        scrollbar-darkshadow-color:#fff;
        }
        -->
        ＜/style>

-  为什么无法定义1px左右高度的容器

        IE6下这个问题是因为默认的行高造成的,解决的技巧也有很多：
        例如:overflow:hidden 　 zoom:0.08 　 line-height:1px


## javascript

-  HTML对象获取问题

        FireFox：document.getElementById("idName");
        ie:document.idname或者document.getElementById("idName").
        解决办法：统一使用document.getElementById("idName");

-  const问题

        说明:Firefox下,可以使用const关键字或var关键字来定义常量;
        IE下,只能使用var关键字来定义常量.
        解决方法： 统一使用var关键字来定义常量

-  event.x与event.y问题


        说明:IE下,event对象有x,y属性,但是没有pageX,pageY属性;
        Firefox下,event对象有pageX,pageY属性,但是没有x,y属性.
        解决方法：使用mX(mX   =   event.x   ?   event.x   :   event.pageX;)来代替IE下的event.x或者Firefox下的event.pageX.

-  window.location.href问题

        说明:IE或者Firefox2.0.x下,可以使用window.location或window.location.href;
        Firefox1.5.x下,只能使用window.location.
        解决方法：使用window.location来代替window.location.href.

-  frame问题

        <frame   src="xxx.html"   id="frameId"   name="frameName"   />
        (1)访问frame对象:
        IE:使用window.frameId或者window.frameName来访问这个frame对象.   frameId和frameName可以同名。
        Firefox:只能使用window.frameName来访问这个frame对象.
        另外，在IE和Firefox中都可以使用window.document.getElementById("frameId")来访问这个frame对象.
        (2)切换frame内容:
        在 IE和Firefox中都可以使用window.document.getElementById("testFrame").src   =   "xxx.html"或window.frameName.location   =   "xxx.html"来切换frame的内容.
        如果需要将frame中的参数传回父窗口(注意不是opener,而是parent   frame)，可以在frame中使用parent来访问父窗口。例如：parent.document.form1.filename.value="Aqing";

-  模态和非模态窗口问题

        说明:IE下,可以通过showModalDialog和showModelessDialog打开模态和非模态窗口;Firefox下则不能.
        解决方法：直接使用window.open(pageURL,name,parameters)方式打开新窗口。
        如果需要将子窗口中的参数传递回父窗口,可以在子窗口中使用window.opener来访问父窗口.
        例如：var   parWin   =   window.opener;   parWin.document.getElementById("Aqing").value   =   "Aqing";

-  firefox与IE的父元素(parentElement)的区别

        IE：obj.parentElement
        firefox：obj.parentNode
        解决方法:   因为firefox与IE都支持DOM,因此使用obj.parentNode是不错选择.

-  document.formName.item(”itemName”) 问题

        问题说明：IE下，可以使用 document.formName.item(”itemName”) 或 document.formName.elements ["elementName"]；Firefox 下，只能使用document.formName.elements["elementName"]。
        解决方法：统一使用document.formName.elements["elementName"]。

-  集合类对象问题

        问题说明：IE下，可以使用 () 或 [] 获取集合类对象；Firefox下，只能使用 [ ]获取集合类对象。
        解决方法：统一使用 [] 获取集合类对象

-  自定义属性问题

        问题说明：IE下，可以使用获取常规属性的方法来获取自定义属性，也可以使用 getAttribute() 获取自定义属性；Firefox下，只能使用 getAttribute() 获取自定义属性。
        解决方法：统一通过 getAttribute() 获取自定义属性

-  input.type属性问题


        问题说明：IE下 input.type 属性为只读；但是Firefox下 input.type 属性为读写。
        解决办法：不修改 input.type 属性。如果必须要修改，可以先隐藏原来的input，然后在同样的位置再插入一个新的input元素

-  event.srcElement问题


        问题说明：IE下，even对象有srcElement属性，但是没有target属性；Firefox下，even对象有target属性，但是没有srcElement属性。
        解决方法：使用srcObj = event.srcElement ? event.srcElement : event.target;

-  body载入问题

        问题说明：IE下，使用 document.body.onload = inject; 其中function inject()在这之前已被实现；在Firefox下，使用 document.body.onload = inject();
        解决方法：统一使用 document.body.onload=new Function(’inject()’); 或者 document.body.onload = function(){/* 这里是代码 */}
        [注意] Function和function的区别。

-  innerText在IE中能正常工作，但在FireFox中却不行.

        需用textContent。
        解决方法:
        if(navigator.appName.indexOf("Explorer")   >   -1){
                document.getElementById('element').innerText   =   "my   text";
        }   else{
                document.getElementById('element').textContent   =   "my   text";
        }

-