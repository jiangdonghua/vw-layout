# fly-pig

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


```
// https://github.com/michael-ciniawsky/postcss-load-config

module.exports = {
  "plugins": {
    "postcss-import": {},
    "postcss-url": {},
    "postcss-aspect-ratio-mini": {},
    "postcss-write-svg": {
      utf8: false
    },
    "postcss-cssnext": {},//让我们使用CSS未来的特性，其会对这些特性做相关的兼容性处理
    "postcss-px-to-viewport": { //用来把px单位转换为vw、vh、vmin或者vmax这样的视窗单位，也是vw适配方案的核心插件之一
      viewportWidth: 750,     // (Number) The width of the viewport.视窗的宽度，对应的是我们设计稿的宽度，一般是750
      viewportHeight: 1334,    // (Number) The height of the viewport. 视窗的高度，根据750设备的宽度来指定，一般指定1334，也可以不配置
      unitPrecision: 3,       // (Number) The decimal numbers to allow the REM units to grow to. 指定`px`转换为视窗单位值的小数位数（很多时候无法整除）
      viewportUnit: 'vw',     // (String) Expected units.指定需要转换成的视窗单位，建议使用vw
      selectorBlackList: ['.ignore', '.hairlines'],  // (Array) The selectors to ignore and leave as px.指定不转换为视窗单位的类，可以自定义，可以无限添加,建议定义一至两个通用的类名
      minPixelValue: 1,       // (Number) Set the minimum pixel value to replace.小于或等于`1px`不转换为视窗单位，你也可以设置为你想要的值
      mediaQuery: false       // (Boolean) Allow px to be converted in media queries.允许在媒体查询中转换`px`
    },
    "postcss-viewport-units": {},
    "cssnano": {              //主要用来压缩和清理CSS代码 Webpack中，cssnano和css-loader捆绑在一起，所以不需要自己加载它
      preset: "advanced",
      autoprefixer: false,
      "postcss-zindex": false //把autoprefixer和postcss-zindex禁掉了。前者是有重复调用，后者是一个讨厌的东东。只要启用了这个插件，z-index的值就会重置为1。这是一个天坑，千万记得将postcss-zindex设置为false。
    },
    // to edit target browsers: use "browserslist" field in package.json
    // "autoprefixer": {}由于cssnext和cssnano都具有autoprefixer,事实上只需要一个，所以把默认的autoprefixer删除掉，然后把cssnano中的autoprefixer设置为false。
  }
}


//目前出视觉设计稿，我们都是使用750px宽度的，那么100vw = 750px，即1vw = 7.5px。那么我们可以根据设计图上的px值直接转换成对应的vw值。在实际撸码过程，不需要进行任何的计算，直接在代码中写px，
//   .test {
//     border: .5px solid black;
//     border-bottom-width: 4px;
//     font-size: 14px;
//     line-height: 20px;
//     position: relative;
//   }
//   [w-188-246] {
//     width: 188px;
//   }
//编译出来的CSS：
//   .test {
//     border: .5px solid #000;
//     border-bottom-width: .533vw;
//     font-size: 1.867vw;
//     line-height: 2.667vw;
//     position: relative;
//   }
//   [w-188-246] {
//     width: 25.067vw;
//   }

//在不想要把px转换为vw的时候，首先在对应的元素（html）中添加配置中指定的类名.ignore或.hairlines(.hairlines一般用于设置border-width:0.5px的元素中)：
//   <div class="box ignore"></div>
//写CSS的时候：
// .ignore {
//   margin: 10px;
//   background-color: red;
// }
// .box {
//   width: 180px;
//   height: 300px;
// }
// .hairlines {
//   border-bottom: 0.5px solid red;
// }

//编译出来的CSS:
//   .box {
//     width: 24vw;
//     height: 40vw;
//   }
//   .ignore {
//     margin: 10px; /*.box元素中带有.ignore类名，在这个类名写的`px`不会被转换*/
//     background-color: red;
//   }
//   .hairlines {
//     border-bottom: 0.5px solid red;
//   }

//上面解决了px到vw的转换计算。那么在哪些地方可以使用vw来适配我们的页面。根据相关的测试：

// 容器适配，可以使用vw
// 文本的适配，可以使用vw
// 大于1px的边框、圆角、阴影都可以使用vw
// 内距和外距，可以使用vw

//postcss-aspect-ratio-mini 主要用来处理元素容器宽高比。在实际使用的时候，具有一个默认的结构

// <div aspectratio>
//   <div aspectratio-content></div>
// </div>

//在实际使用的时候，你可以把自定义属性aspectratio和aspectratio-content换成相应的类名，比如：


// <div class="aspectratio">
//   <div class="aspectratio-content"></div>
// </div>


//我个人比较喜欢用自定义属性，它和类名所起的作用是同等的。结构定义之后，需要在你的样式文件中添加一个统一的宽度比默认属性：

// [aspectratio] {
// position: relative;
// }
// [aspectratio]::before {
//   content: '';
//   display: block;
//   width: 1px;
//   margin-left: -1px;
//   height: 0;
// }
//
// [aspectratio-content] {
//   position: absolute;
//   top: 0;
//   left: 0;
//   right: 0;
//   bottom: 0;
//   width: 100%;
//   height: 100%;
// }

//如果我们想要做一个188:246（188是容器宽度，246是容器高度）这样的比例容器，只需要这样使用：

//   [w-188-246] {
//     aspect-ratio: '188:246';
//   }

//有一点需要特别注意：aspect-ratio属性不能和其他属性写在一起，否则编译出来的属性只会留下aspect-ratio的值，比如：

//  <div aspectratio w-188-246 class="color"></div>

//编译前的CSS如下：

// [w-188-246] {
//   width: 188px;
//   background-color: red;
//   aspect-ratio: '188:246';
// }

//编译之后：

// [w-188-246]:before {
//   padding-top: 130.85106382978725%;
// }


//主要是因为在插件中做了相应的处理，不在每次调用aspect-ratio时，生成前面指定的默认样式代码，这样代码没那么冗余。所以在使用的时候，需要把width和background-color分开来写：

// [w-188-246] {
//   width: 188px;
//   background-color: red;
// }
// [w-188-246] {
//   aspect-ratio: '188:246';
// }

//这个时候，编译出来的CSS就正常了：


// [w-188-246] {
//   width: 25.067vw;
//   background-color: red;
// }
// [w-188-246]:before {
//   padding-top: 130.85106382978725%;
// }

//目前采用PostCSS插件只是一个过渡阶段，在将来我们可以直接在CSS中使用aspect-ratio属性来实现长宽比。


//宽高比相关的详细介绍 https://www.w3cplus.com/css/aspect-ratio.html  https://www.w3cplus.com/css/aspect-ratio-boxes.html https://www.w3cplus.com/css/experiments-in-fixed-aspect-ratios.html https://www.w3cplus.com/css/css-polyfluidsizing-using-calc-vw-breakpoints-and-linear-equations.html


//postcss-write-svg 用来处理移动端1px的解决方案 主要使用的是border-image和background来做1px的相关处理。比如：

//     @svg 1px-border {
//       height: 2px;
//       @rect {
//         fill: var(--color, black);
//         width: 100%;
//         height: 50%;
//       }
//     }
//     .example {
//       border: 1px solid transparent;
//       border-image: svg(1px-border param(--color #00b1ff)) 2 2 stretch;
//     }

//编译出来的CSS:

// .example {
//     border: 1px solid transparent;
//     border-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' height='2px'%3E%3Crect fill='%2300b1ff' width='100%25' height='50%25'/%3E%3C/svg%3E") 2 2 stretch;
//   }

//上面演示的是使用border-image方式，除此之外还可以使用background-image来实现。比如：

// @svg square {
//   @rect {
//     fill: var(--color, black);
//     width: 100%;
//     height: 100%;
//   }
// }
//
// #example {
//   background: white svg(square param(--color #00b1ff));
// }

//编译出来就是：

// #example {
//   background: white url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Crect fill='%2300b1ff' width='100%25' height='100%25'/%3E%3C/svg%3E");
// }

//由于有一些低端机对border-image支持度不够友好，个人建议你使用background-image的这个方案。


// CSS Modules
// Vue中的vue-loader已经集成了CSS Modules的功能，个人建议在项目中开始使用CSS Modules。


// postcss-viewport-units    插件主要是给CSS的属性添加content的属性，配合viewport-units-buggyfill库给vw、vh、vmin和vmax做适配的操作。
// 这是实现vw布局必不可少的一个插件，因为少了这个插件，这将是一件痛苦的事情。后面你就清楚。

// 到此为止，有关于所需要的PostCSS已配置完。并且简单的介绍了各个插件的作用，至于详细的文档和使用，可以参阅对应插件的官方文档。

```
