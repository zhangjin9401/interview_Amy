# 一.浮动
 ## 1.核心
    浮动元素会脱离文档流向左／向右浮动，直到碰到父原素或另一个浮动元素；
 ## 2.问题
    -1 可以实现类似inline-block的布局，但是每个浮动元素高度不定时，会出现卡住的问题;(原因：遇到了另一个浮动元素)
    -2 导致高度塌陷，父元素没有高度；
 ## 3.清除浮动（clear清除和BFC清除两种方式）
    -1 clear是加在父元素上的，不是加在浮动元素上的；
        .clearfix:after{
            content:'';
            display:block;
            height:0;
            clear:both;
            visibility:hidden;
        }
    -2 父级元素是BFC(块级格式化上下文)
        -1 拥有display：不为block;
        -2 拥有position:不为relative;
        -3 拥有overflow:hidden | auto | scroll
        -4 拥有float:left;
    总结：常规的多列布局用inline-block;自适应的多列布局用浮动；
    -3 给浮动元素本身后加一个空div,设置clear:both;
    -4 给父容器紧邻的元素添加clear:both;

# 二，css3新增
# 三，实现居中
 ## 1,text-align:
    设置块级元素内文本(或行内元素有效, img标签也可以)的水平对齐方式；（对块级元素内的块集元素无效），即此属性是加在块级元素上的；
 ## 2,line-height:
    用来设置文字的垂直居中
 ## 3，vertical-align:
    定义行内元素基线对于该元素所在行的基线的对齐方式，
    用法：
    一：父元素设置height和line-height,子元素设置inline-block,vertical-align
    .p{
        height:400px;
        line-height:400px;
    }
    .c{
        display:inline-block;
        vertical-align:middle;
    }
    二：若未对父元素设置line-height,对两个行内元素同时加vertical-align:middle;可使两元素居中对奇

 ## 4，水平居中
    1，行内：text-align:center
    2, 块级：margin:0 auto;
    3, 多个块级元素水平居中：实现在一列的li;li{display:inline-block} ul{text-align:center;font-size:0}
 ## 5，垂直居中
    一，对于不知宽高的元素
     -1 父元素设line-height;子元素设vertical-align,display:inline-block
     -2 父元素display:table-cell；vertical-align:middle;子元素设置display:inline-block
# 四，两栏布局
    两栏即定宽／不定宽 +自适应
    最见单的方法：左float:left +右：display:table-cell
    还可以左float:left+右overflow:hidden
# 五，等宽等高的三列布局

