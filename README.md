# CSSPOLY
> CSS兼容主流浏览器引擎的SCSS拓展库

目前还有很多css属性还未标准化，主流的浏览器引擎引用该属性的时候还需要添加对应的引擎前缀，这样无疑会增加代码量。因此如果你常用SCSS来设计样式的话，可以考虑引用这个csspoly拓展库。它主要的功能就是将需要添加前缀的属性重写成@mixin方法，在需要的地方调用即可，方法名称和属性命名相同，而且参数类型一致。

  - 常见的css3属性
  - 浏览器引擎选择
  - 相同命名规则及参数类型
  - 参数单一单位略写

## 引用

  - 单文件引入
  - 自定义重写方法引入
  ##### 单文件引入
  只需要在你的SCSS文件中引用该库即可
  ``` scss
  @import "[Your Project Path]/dist/csspoly";
  ```
  ##### 自定义重写方法引入
  将整个库项目下载下来，修改scss/func/目录下的方法文件，然后再scss目录下修改csspoly入口文件即可。
  ``` scss
  @import "[Your Project Path]/scss/csspoly";
  ```

## 配置
根据开发场景可自定义需要编译的浏览器引擎，在csspoly入口文件里修改。如果确定应用场景，如基于webkit引擎开发的应用，那么其它浏览器引擎变量可以设置为false，这样对应的前缀不会被编译，减少代码量。

| 变量      | 类型    | 默认值 | 说明                       |
| --------- | ------- | ------ | -------------------------- |
| Mozilla   | Boolean | true   | 是否编译Firefox前缀        |
| Webkit    | Boolean | true   | 是否编译Chrome和Safari前缀 |
| Opera     | Boolean | true   | 是否编译Opera前缀          |
| Microsoft | Boolean | true   | 是否编译IE前缀             |

## 示例

引用方式跟常规css属性一样，只不过在SCSS文件中，需要添加@include前缀，方法名称一致，单一单位必须略写，例如30deg直接写30即可。

例：利用rotate() 方法让div旋转30度

```scss
div{
  display: block;
  width: 100px;
  height: 50px;
  background-color: #ddd;
  @include rotate(30);
}
```

编译结果：

```css
div{
  display: block;
  width: 100px;
  height: 50px;
  background-color: #ddd;
  -o-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  -moz-transform: rotate(30deg);
  -webkit-transform: rotate(30deg);
  transform: rotate(30deg); 
}
```



## 强调

所有方法中，若参数单位是唯一的，必须略写！例如角度（deg），时间（s）等。多种单位的方法必须跟随单位，例如尺寸（px），百分比（%）。
