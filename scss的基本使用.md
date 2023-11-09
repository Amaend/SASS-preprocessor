## 1.scss的基本使用
#### scss的变量命名
scss的变量命名通过$符号进行命名
``` javascript
$primary-color:red
$primary-border:1px solid $primary-color
```
 可以实现嵌套变量使用
 #### scss的嵌套使用
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

可以通过添加&的符号实现选择父类选择器，实现添加伪类及伪元素
