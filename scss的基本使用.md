## scss的基本使用
### scss属性及基本用法
#### scss的变量命名
scss的变量命名通过$符号进行命名
``` scss
$primary-color:red
$primary-border:1px solid $primary-color
```
 可以实现嵌套变量使用
 #### scss的嵌套使用
 可以通过添加&的符号实现选择父类选择器，实现添加伪类及伪元素
``` html
<body>
    <diu>
    	<ul>
            <li></li>
        </ul>
    </diu>
</body>
<style>
    div{
        width:200px;
        ul{
            marjin:0;
            li{
                font-size:12px;
                color:pink;
                &:hover{
                    color:#ff6700;
                }
            }
        }
    }
</style>
```
#### scss的属性嵌套
可以通过对相同的属性进行属性嵌套的写法（但是属性嵌套必须在属性后面添加：）

``` scss
div{
    marjin: 0 {
        left:10px;
        right:10px
    }
    ul{
        li{
            font:{
                size:12px;
                color:red;
            }
        }
    }
}
```
### scss的mixin的基本使用

混合指令（Mixin）用于定义可重复使用的样式，避免了使用无语意的 class，比如 .float-left。混合指令可以包含所有的 CSS 规则，绝大部分scss规则，甚至通过参数功能引入变量，输出多样化的样式。
#### 定义混合指令Mixin

同时mixin也可以实现标签嵌套

``` scss
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
  a{
        color:#ff6700;
    }
}
```

#### mixin的使用

 使用 @include 指令引用混合样式，格式是在其后添加混合名称，以及需要的参数（可选）。

``` scss
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```

#### mixin的嵌套使用

``` scss
@mixin compound {
  @include highlighted-background;
  @include header-text;
}
@mixin highlighted-background { background-color: #fc0; }
@mixin header-text { font-size: 20px; }
```

#### mixin的参数

参数用于给混合指令中的样式设定变量，并且赋值使用。在定义混合指令的时候，按照变量的格式，通过逗号分隔，将参数写进圆括号里。引用指令时，按照参数的顺序，再将所赋的值对应写进括号。

``` scss
@mixin alter($color,$width){
    border:{
        color:$color;
        width:$width;
        styly:#000;
    }
}
div{
    @include alter(#ff6700,2px)
}
```

**同时也可以给参数添加默认参数**

``` scss
div{
    @include alter($color:blue,$width:2px)
}
```

### scss的extend的基本用法

#### extend的定义

@extend 指令告诉 Sass 一个选择器的样式从另一选择器继承。
如果一个样式与另外一个样式几乎相同，只有少量的区别，则使用 @extend 就显得很有用。

``` scss
.contanier1{
  font-size: 24px;
  font-weight: bold;
  color: green;
}
.contanier2{ 
  @extend .contanier1;
  color: red;
}
.contanier3{ 
  @extend .contanier1;
  font-size: 30px;
}
```

#### 继续延伸

当一个选择器延伸给第二个后，可以继续将第二个选择器延伸给第三个

``` scss
.normai_error{
    text-decoration: none;
    font-size: 18px;
    background-color: #f00;
}
.task_error{
    @extend .task_error;
    width: 200px;
    height: 400px/960px*100%;
    background-color: #0f0;
}
.error_box{
    @extend .task_error;
    position: absolute;
    left: 0;
    bottom: 0;
}
```

### scss的import的基本用法

 CSS有一个 @import 规则，可以在一个css文件中导入其他css文件，然而这样会有一个弊端：只有执行到@import 语句所在行的之后，浏览器才会去加载相应的css文件，这会导致页面加载变慢。而Sass在css的基础上改进了@import 规则，但你在.sass/.scss 文件中 通过@import引用样式文件时，它就会在编译成css文件时，就把相关文件导入，相当于所有相关的样式被归纳到了一个css文件中，浏览器只需发起一次加载请求。

 @import 导入的规则，可以使样式的可重用性变得更高。并且被导入文件中的变量和混合器也都可在导入文件中使用。

#### 定义@import导入

```scss
/* 导入colors.scss */
@import "colors"
/* 导入mixins.sass */
@import "mixins"
```

#### 局部文件

 在项目中，有很多的 .sass/.scss 文件，我们并不想让他单独编译成一个css文件，只是想将其作为一个工具文件，在其他的 .sass/.scss 文件中，通过@import 引用。这样的文件，就称为局部文件。局部文件可以在多个文件中被引用。

 我们通常约定这样的局部文件，命名以下划线开头，这样sass就不会在编译时单独编译这个文件输出css，而只把这个文件用作导入。而且当 @import 引入这类文件时，可以省略文件名开头的下划线。

```scss
/* 导入 _fonts.scss */
@import "fonts"
```

### scss注释的基本使用

#### 单行注释

``` scss
//用“//”即可实现单行注释，当行注释不会在css编译中出现
```

#### 多行注释

``` scss
/*多行注释
*多行注释会在css编译时出现
*/
```



