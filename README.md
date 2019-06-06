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
    $refs只会在组件渲染完成之后生效，并且它们不是响应式的。这仅仅是一个用于直接操作子组件的“逃生舱”，应该避免在模板(?)或计算属性(?)中访问$ref
    
