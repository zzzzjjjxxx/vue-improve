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
