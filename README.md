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
    
# 如何复用组件，比如说进入同一个页面，需要根据传递进去不同的参数，来做不同的做法
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
    isEdit: { // create的时候为false，edit为true
      type: Boolean,
      default: false
    }
  },
