# sftx-comm-control

[![Latest Version on NPM](https://img.shields.io/npm/v/sftx-comm-control.svg?style=flat-square)](https://npmjs.com/package/sftx-comm-control)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://api.travis-ci.org/Dickkk/sftx-comm-control.svg?branch=master)](https://travis-ci.org/Dickkk/sftx-comm-control)
[![npm](https://img.shields.io/npm/dt/sftx-comm-control.svg?style=flat-square)](https://www.npmjs.com/package/sftx-comm-control)

## 说明
vue的业务组件库，对一些公共的业务组件抽离成单独的npm模块，业务系统公用。
## 关于测试
基于jest，在发布前会进行dom与快照的基本测试，开发组件的时候需要同时把单元测试完善。

## 安装、发布步骤
``` bash
# 安装
npm install

# 发布
npm run pub

# 测试
npm run test
```

## 业务工程使用说明
安装依赖
```
npm i sftx-comm-control -S
```
引用
```
import {Expression} from 'sftx-comm-control';
```
全局注册
```
Vue.use(Expression.name,Expression);
```
局部注册
```
const vueapp=new Vue({
    el: '#app',
    components: { Expression },
    template: '<Expression/>'
})
```
## 目录
```
.
├── README.md
├── __tests__                 # jest 测试程序目录
│   ├── Expression.test.js
│   ├── __snapshots__
│   │   └── Expression.test.js.snap
│   └── helpers
│       └── LocalStorageMock.js
├── lib                       # es5入口
│   └── index.js
├── package-lock.json
├── package.json
├── src                       # 代码目录
│   ├── assets
│   ├── components
│   │   ├── Expression.vue
│   │   ├── Tab.vue
│   │   └── Tabs.vue
│   └── index.js              #es6+ 入口，程序主入口
├── webpack.base.js
└── webpack.config.js
```

 ***

## 组件

### Expression表达式
***

> script直接引入方式 demo在test/express目录

1、  引入script

    <script src="sftx-comm-control/lib/index.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
2、  初始化
```
const ops=[{name:"交易金额",value:"txAmt"},{name:"开户金额",value:"opnAmt"}];
const exps=[{name:"加",value:"+"},{name:"减",value:"-"}];

function save(result){
    alert('new result='+result);
    //根据result做逻辑处理
    //关闭窗口
}
function cancle(){
    alert('new cancle');
    //关闭窗口
}
var data='txAmt+1+3+txAmt+4^2';
var vm=sftxCommControl.ExpressionApp('#app',ops,'name','value',exps,save,cancle,data);
vm.data='txAmt+opnAmt';
```

  第一个参数'#app'是标签的id，第二个标签'ops'是因子数组，第三个参数'name'是因子数组中显示在下拉框的值，
value:因子的值，exps:自定义表达式，格式是[{name:' ',value: ' '}]，save是点击保存的回调函数。cancle
是点击取消的回调函数，data是初始化组件的表达式。返回的是vm， 可以通过修改vm.data属性，动态改变表达式。

> webpack方式引入

webpack方式就是引入的方式不一样，通过npm commonjs方式直接引用。其他参数、用法一样。
```
import {ExpressionApp} from 'sftx-comm-control';
var vm =ExpressionApp('#app',ops,'name','value',exps,save,cancle,data);
```





