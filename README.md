# vue-improve
Vue.set(data,'sex', '男')是为对象中某个属性值动态生成的动态生成方式
data = {
    name: "简书",
    age: '3',
    info: {
        content: 'my name is test'
    }
# 1
  list.forEach(e => {
            this.list.push(e)
          })
             list.map(item => {
          if (!item.correspondUser || !item.correspondUser.name) {
            item.correspondUser = { name: '未完善' }
          }
        })一个修改item，一个修改list
# 2
`您好！我是${this.companyName}的${this.name},这是我的名片`要用到data里的数据的时候，放在一个字符串里，可以这么写
# 3 if{查询列表的数据} else {
        wx.showToast({
          title: message,
          icon: 'none',
          duration: 2000
        })要是没有查到做一个判断
# 4 更新数据的时候，最简单的方法是通过 .length来判断是否符合要求，再进行提交操作
# 5 JS将秒换成时分秒 formatSeconds
# 6 :class="{active:(index===1)}"根据index来确定是否进行某个样式的绑定
# 7 对比可以看出v-if直接从代码中删除了，v-show只是通过display来切换状态，因此建议频繁切换的话用v-show比较好
# 8  watch: {
    'a': function (val, oldVal) {
      console.log(val, oldVal,(val== oldVal))
    },
# 9 
var vm = new Vue({
  data: {
    a: 1,
        c:{
            c1:1,
            c2:2
        }
  },
  watch: {
    'a': function (val, oldVal) {
      console.log(val, oldVal,(val== oldVal))
    },
    // 方法名
    'b': 'someMethod',
    // 深度 watcher
    'c': {
      handler: function (val, oldVal) { 
            console.log(val, oldVal,(val== oldVal))
            },
      deep: true
    }
  }
})
        
vm.a = 2 
vm.c.c1 = 2
--------------------- 
作者：蜗牛速度额 
来源：CSDN 
原文：https://blog.csdn.net/weixin_41111068/article/details/83046691 
版权声明：本文为博主原创文章，转载请附上博文链接！
和深度无关，而是在修改（不是替换）对象或数组时，旧值将与新值相同，因为它们索引同一个对象/数组。
# 10 根据传过来的type的变化来更新
 data (newValue, oldValue) {
      if (newValue.type !== oldValue.type) {
        wx.reLaunch({
          url: this.url
        })
      }
    }
# 11 组件里面的两种方法好像是一样的，都是从父页面引用过来，或者
   if (item.data.product.name === '地图导航') {
          this.$emit('getAddress')
          this.getAddress()
        } else if (item.data.product.name === '联系电话') {
          this.makePhoneCall()
          this.$emit('makePhoneCall')
        }上面是我的猜测
          if (item.data.product.name === '地图导航') {
          this.$emit('getAddress')// 父页面有这个方法
        } else if (item.data.product.name === '联系电话') {
          this.makePhoneCall() // 父页面没有这个方法，但是其他页面有，多处都定义了
        }是真实的内容，
 # 12
   this.$emit('productId', [item.data.product.id, jumpType])对应父页面里面 <swiperWan @productId="getJumpWay" :data="item.data" v-if="item.name==='wSlider'" url="../loading/index"></swiperWan>的方法是写出来的，   
   getJumpWay (data) {
      if (data[1] === 1) {
        wx.navigateTo({
          url: '../product/detail/index?id=' + data[0]
        })
      } else if (data[1] === 2) {
        wx.navigateTo({
          url: `../../packageA/pages/customPage/index?id=${data[0]}`
        })
      }其中data[0],data[1],分别对应两个参数
      
    },
# 13 因为本来我写在页面里面，是通过this.flag来判断的，但是现在还有一个办法就是，往列表的元素里面 通过this.$set()来添加元素
    // 结束视频播放的时候
    videoStop (item) {
      this.$set(item, 'videoFlag', false)
      this.$set(item, 'videoContext', null)
    },
    // 播放视频
    videoPlay (id, item) {
      this.data.list.map(child => {
        this.$set(child, 'videoFlag', false)
        this.$set(child, 'videoContext', null)
      })
      this.$set(item, 'videoFlag', true)
      this.$set(item, 'videoContext', wx.createVideoContext(id))
      item.videoContext.play()
    }
# 14 页面里面变量的写法
`top: ${stickyTop}px; z-index: ${zIndex}`
# 15  if (!response.data.items) return
在我们获取列表的时候，进行对列表先处理判断，防止列表为空，报错等等
# 16 根据点击到这个页面，进入这个页面传递过来的参数对表单=》进行不同的处理
this.postForm = Object.assign({}, defaultForm)是对页面所有的表单进行置空的操作
const defaultForm = {
  name: '',
  id: '',
  title: '',
  substance: '',
  imgUrl: '',
  type: 1,
  content: ''
}
<el-form ref="postForm" :model="postForm" class="form-container">等等
    
# 17 在更新一个数据的时候，或者保存提交发布一个数据的时候，需要对返回的状态code===200或400进行判断，处理着来做一个提示
     updateItem(this.postForm).then(response => {
              if (response.data.code === 200) { 
                this.loading = true //如果发布成功，就不要进行一个loading框的显示
                this.$notify({ 
                  title: '成功',
                  message: '发布成功',
                  type: 'success',
                  duration: 2000
                })
                this.$router.replace({ path: '/article/list' }) // 进行一个成功之后的跳转 <el-button v-loading="loading" class="save" @click="submitForm">保存</el-button>一开始是false
              } else {
                this.loading = false 
              }
              this.loading = false
            })
    
# 18 如何复用组件，比如说进入同一个页面，需要根据传递进去不同的参数，来做不同的做法
<template>
  <article-detail :is-edit="true"/>
</template>
<script>
import ArticleDetail from './components/ArticleDetail'
export default {
  name: 'EditForm',
  components: { ArticleDetail }
}
</script> // 它是往ArticleDetail这个组件里面传递了一个is-edit（等于isEdit）这个参数
// 以下是ArticleDetail里接收父组件传过来的内容
  props: {
    isEdit: { // create的时候为false，edit为true,在子组件里面用来接收传过来的参数，可以使用
      type: Boolean,
      default: false
    }
  },
# 19小程序复用组件
async selectRanking () {
  const { data: { RankingList: { list, nextPage, pageNum, lastPage } } } = await apicustom.selectRanking({pageNum:this.pageNum,pageSize:this.pageSize })
        this.persons = list
        // this.person = this.personslist.slice(1, (this.personslist.length))
        this.lastPage = lastPage // 先在这里获取最后一页
        this.pageNum = pageNum // page当前页面码
        this.nextPage = nextPage // 下一页的页码数
        if (this.pageNum === 1) { // 如果只是请求第一页面的数据的话，就把显示的列表，赋值为所有获取到的数据
          this.personslist = this.persons
          this.avatarUrlFirst = this.personslist[0].avatarUrl ? this.personslist[0].avatarUrl:'https://oss.wq1516.com/defaultavatar.png'
          this.nameFirst = this.personslist[0].name ? this.personslist[0].name : 0
          this.bindingNumFirst = this.personslist[0].bindingNum ? this.personslist[0].bindingNum : 0
          this.praiseNumFirst = this.personslist[0].praiseNum ? this.personslist[0].praiseNum : 0
        } else { // 如果获取的不是第一页的内容的话，就要把获取到的数据，加到你所要展示的数据上去
          this.persons.forEach(e => {
            this.personslist.push(e)
          })
        }
      }
// 上拉加载
async onReachBottom () {
  if (this.pageNum < this.lastPage) { // 如果当前页面小于最后一页
        this.pageNum = this.nextPage // 把当前页面，变成下一页面的页面数
        this.selectRanking() // 进行对后台数据的请求
      } else {
        wx.showToast({ // 如果当前页面处于最后一页，就提示没有数据了
          title: '没有更多了',
          icon: 'none',
          duration: 2000
        })
      }
    },
    // 下拉刷新
    async onPullDownRefresh () {
      this.pageNum = 1 // 只请求第一页面的列表数据
      this.selectRanking() // 进行数据的请求
      wx.stopPullDownRefresh() // 停止下拉刷新
    },
    onLoad () {
      this.pageNum = 1 // 刚进入页面的时候，只请求第一页的数据
      this.selectRanking() // 进行数据加载
    },
    // 
data:{ 
        pageNum: 1,
        lastPage: 100,
        nextPage: 1,
        pageSize: 6
        }
        
# 19 ref用来访问子组件实例或者子元素
尽管有Prop和事件，有的时候你仍然可能需要在JavaScript里直接访问一个子组件，为了达到这个目的，可以通过ref特性为这个子组件赋予一个id引用
例如<base-input ref="usernameInput"></base-input>现在定义了这个ref的组件里，可以使用
this.$refs.usernameInput来访问这个<base-input>实例
    程序化地从一个父组件聚焦在这个输入框
<base-input>组件也可以用一个类似的ref提供对内部这个指定元素的访问？
甚至可以通过其他父级组件定义方法
    // 子组件的写法
    <base-input ref="usernameInput"><input ref="input"></base-input>
    methods:{
    focus:function (){
    this.$refs.input.focus()
}
    }
    // 父组件的调用方法
    this.$refs.usernameIput.focus()
    ----------
    当ref和v-for一起用的时候，你得到的引用将会是一个包含了对应数据源的这些子组件的数组
    <div v-for="item in list" ref="list">
        <h1>{{item}}</h1>
    </div>
    父组件里我对它进行一个引用，this.$refs.list得到的是
    <div><h1>{{item1}}</h1></div>
    <div><h1>{{item2}}</h1></div>
    <div><h1>{{item3}}</h1></div>
    --------------
    $refs只会在组件渲染完成之后生效，并且它们不是响应式的。这仅仅是一个用于直接操作子组件的“逃生舱”，应该避免在模板(这是响应式的?)或计算属性(这是响应式的?)中访问$ref
    
# 20 内联模板
当 inline-templete这个特殊的特性出现在一个子组件上时，这个组件将会使里面的内容作为模板，而不是将其作为发布的内容。
<my-component inline-templete>
    <div>
        <p></p>
    </div>
    </component>
    内联模板需要定义在vue所属的DOM元素内？
    不过，inline-template会让模板的作用域变得更加难以理解。
# X-Template
 另外一个定义模板的方式是在一个<script>元素中，并为其带上 text/x-template的类型，然后通过一个id将模板引用过去
 <script type="text/x-template" id="hello">
     <p></p>
    </script>
    Vue.component('hello-world', {
    template:'#hello'
    })
    x-template需定义在vue所属的DOM元素外？
    
# 计算属性 
模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重而且难以维护
<div id="example">
    {{ message.split('').reverse().join('') }}
    </div>
    在这个地方，模板不再是简单的生命式逻辑。你必须看看一段时间才能意识到，这是想要显示变量message的翻转字符串。当你想要在模板中多次引用此处的翻转字符串时，会更加难以处理，（对于复杂的逻辑，应该使用计算属性）
    -------以下是举例分割线
    <div id="example">
    <p>{{ msg }}</p>
    <p>{{ reversemsg }}</p>
    </div>
    var vm = new Vue({
    data:{
    message: 'hello'
    },
    computed: {
    reversemsg () {
    // this指向vm实例
    return this.message.split('').reverse().join('')
    }
    }
    })
----ref被用来给元素或者子组件注册引用信息，引用信息将会注册在父组件的$refs对象上。
重点！关于ref注册时间，因为ref本身是作为渲染结果被创建的，在初始渲染的时候你不能访问它们，它们还不存在!$refs也不是响应式的，因此你不应该视图用它在模板中做数据绑定
# el
提供一个在页面上已存在的dom元素作为vue的挂载目标。可以是css选择器，也可以是一个htmlelement的实例，
# beforeCreate
在初始化之后，数据观测和event/watcher事件配置之前被调用
# created
数据观测，属性和方法的运算，watch/event事件回调
但是挂载还没开始，$el属性目前不可见
# beforeMounted
在挂载之前被调用：相关的render函数首次被调用
渲期间不被调用
# mounted
el被新创建的$el替换，并挂载到实例上去之后调用该钩子，但是它不承诺把所有子组件一起挂载，
如果希望等到整个视图都渲染完毕，可以用this.$nextTick替换掉mounted
mounted () {
this.$nextTick(function () {
})
# upadated 
由于数据更改导致的虚拟dom重新渲染和打补丁，在这之后会调用这个钩子，所以最好避免在这期间更改状态
# 认识flow
flow是Facebook出品的JavaScript静态类型检查工具。vue.js的源码用flow做了静态类型检查。所以了解flow有助于阅读源码
JavaScript是动态类型语言，它的灵活性好，但是容易写成隐蔽性强的隐患代码，在编译初期不会报错，运行阶段出现bug
类型检查是当前语言类型的发展趋势，类型检查，就是在编译早起尽早发现bug，但是不影响代码运行(不需要运行时候动态类型检查)
项目越复杂越需要通过工具来保证项目的维护性和增强代码的可读性。
vue.js在做2.0重构的时候回，在es2015的基础上，出来eslint保证代码风格之外，引入flow做静态类型检查。之
之所以选择flow，主要是因为在babel和eslint都有对应的flow插件以支持语法，可以沿用构建配置，非常小的成本的改动可以拥有静态类型检查的能力
# babel是什么
babel是一个JavaScript编译器，babel是一个工具链，主要讲ecmascript2015+的版本的代码转化为向后兼容的JavaScript，以便能能够运行当前和旧版本额浏览器
源码转化
通过@polyfill或者@babel模块在目标环境中添加缺失的特性
babel工具链是由大量的工具组成的，这些工具都简化了babel的使用，如果你在使用一套框架，babel可能已经为你配置好了
本指南将向你展示如何在es2015的JavaScript代码编译为能在当前浏览器上工作的代码
配置过程包括1.运行以下命令安装所需要的包
npm install --save-dev @babel/core @babel/cli @babel/preset-env
npm install --save @babel/poyfill
2.在项目的根目录下创建一个名为babel.config.js的配置文件：
const presets = [
[
"@babel/env",
{
targets：{
edge：“17”，
Firefox：“60”，
chrome：“67”，
Safari："11.1"
},
useBuiltIns：“usage”
}
]
]；
module.exports = { presets };
]
3.运行这个命令将src目录下所有代码编译到lib目录：
./node_modules/.bin/babel src --out-dir lib这一句的意思就是可以用npm@5.2.0自带的npm包运行器将
./node_modules/.bin/babel 缩短为npx babel
你所需要的所有的babel模块都是作为独立的npm包发布的，并且这种模块化的设计能让每种工具都针对特定使用情况进行设计
babel的核心功能包含在@babel/core模块中，可以通过以下命令安装:
npm install --save-dev @babel/core
你可以在JavaScript程序中直接require并使用它：
const babel = require（"@babel/core"）;
babel.transform("code",optionsObject);
作为一名最终用户，你可以需要安装其他工具作为@babel/core的使用接口？并很好的集成到你的开发流程中
@babel/cli是能够从终端命令行使用的工具
这能解析src目录下的所有JavaScript文件，并应用我们所指定的代码转化功能，然后把每个文件输出到lib目录下。
由于我们还没有指定任何代码转化功能，所以输出的代码和输入的代码的代码相同（不保留源代码格式），我们可以将我们所需的代码转化功能作为参数传递进去
上述实例中用了--out-dir参数，我可以用 --help参数来查看命令行工具所能接受的所有参数列表（目前最重要的是--plugins和--presets）
（插件和预设preset）
代码转化功能以插件的形式出现，插件是小型的JavaScript程序，用于指导babel如何对代码进行转化，你甚至可以编写自己的插件将你所需的任何代码转化功能应用到你的代码上
代码中有很多残留的es2015的特性，我们希望对它们进行转化，但是不需要一个一个加插件，可以用一个‘preset’（即预先设定的插件）
就像插件一样，可以根据自己所需的插件组合创建一个自己的preset并将其分享出去。
对于当前的用力，可以使用一个名称Wienv的preset
除了上述的方法，也有另外一种支持传递参数的方法：配置文件（在babel.config.js）文件中


# babel 这个编译器简单的工作方式（解析，转化，代码生成）
