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
