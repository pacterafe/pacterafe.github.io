# IDSC编写规范

## 目录

- [编码优化](#code)

- [基础优化](#basc)

- [语义化命名](#semantic)

- [补充说明](#additional)


<h2 id="code">编码优化</h2>

1.组件命名方式

- 首字母大写
- 命名语义化
- 公共组件规范开发Common/Public

2.组件封装严格按照高内聚低耦合原则，拆分到当前组件下components，抽离公共组件。

3.组件内请求分离，api文件内请求对应views/pages组件内容(净化页面请求，把请求处理统一放在api内处理)

4.文件内添加好备注信息
```angular2html
/**
 * @author Lindong
 * @date 2018/8/23
 * @desc File Description
 * @param {Object} [title]  - 参数说明
 * @example 调用示例
 */
```
5.vuex严格按照官方推荐方式，并且拆分五部分
```angular2html
├─store
│  ├─index.js
│  ├─getters.js
│  ├─state,js
│  ├─actions.js
│  ├─mutations.js
│  ├─mutation-types.js
```

6.图标统一使用的是svg和阿里矢量图标库使用方式：symbol引用。组件注入vue跟实例上，直接使用无需引入

7.页面样式禁止使用!important;

8.禁止控制台输出 [黄色] 以及 [红色] 警告和报错信息

9.代码缩进，使用4个空格作为一个缩进层级(请调试好自己使用的编辑器)


<h2 id="basc">基础优化</h2>


1.v-if和v-show的使用场景

- 第一个维度是权限问题，只要涉及到权限相关的展示无疑要用v-if
- 第二个维度在没有权限限制下根据用户点击的频次选择，频繁切换的使用 v-show，不频繁切换的使用 v-if

2.不要在模板里面写过多的判断与表达式
```angular2html
虽然可以识别，但是不宜读，不好维护，建议封装在methods或者computed里面，便于其他相同地方复用
v-if="isFirst && isAadmin && (a||b)"
```

3.使用v-for循环时绑定key唯一值
```angular2html
<ul>
    <li v-for="(item,index) dataList" :key="index"></li>
</ul>
```

4.对路由组件进行懒加载

```angular2html
这里的懒加载是指在访问到对应的组件时才加载它，首屏的时候不加载
const Login = () => import('@/pages/Login')
{ path: '/login', component: () => import('@/views/login/Login'), hidden: true }
```

5.页面如果使用同一逻辑多次需要使用方法进行封装，坚决不允许页面模块内相同方法出现多次

6.初始化页面禁止发送多余的请求，浪费资源


<h2 id="semantic">语义化命名</h2>


语义化命名主要分四类如下：

1、创建组件语义化

- 创建组件语义化命名
- 组件首字母大写

```angular2html
    Loading.vue
    Pagination.vue
```

2、CSS语义化

- CSS类名需要语义化命名
- 禁止使用ID来添加样式
- 重申一遍，样式使用scss语法，以及scss变量
- 修改的公共样式一定要添加好注释信息

3、HTML语义化

- 所有标签均使用语义化标签如、section/acticle/aside/main/header/footer/nav
- 杜绝随便使用div，空盒子包裹可以使用div

4、JS命名语义化

- 变量语义化命名
- 方法需要命名语义化
```实例
    dataList: []        //数据列表
    tableHeader: []     //表格头部数据
    tableBody: []       //表格内容数据
    
    
    handleClick(){}     //手动点击按钮事件
    handleSearch(){}    //手动查询事件
```
以上例子，均起到举一反三的目的！

注：语义化命名坚决不能使用随便语义，要根据使用场景来确定语义名称

<h2 id="additional">补充说明</h2>

1、删除多余的空行

2、删除多余的注释

- 删除注释掉的代码
- 删除没有意义的注释

3、删除多余的方法

- 如果该方法没有使用到，务必删除保证页面整洁
- 如果方法没有执行任何业务逻辑，请删除它或者给出一定注释

4、删除未被使用的资源文件

5、删除多余console

6、添加必要的注释

- 所有自定义的方法需要给出注释
- 比较大的代码块外层需要给出整体注释，且内部逻辑需要添加详细注释
- 所有代码中出现的阿拉巴数字需要给出注释
- 程序中出现加密/解密逻辑的操作地方，需要给出注释说明过程

[前端团队代码评审 CheckList 清单](https://juejin.im/post/5d1c6550518825330a3bfa01)
