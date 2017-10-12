---
layout: post
title:  "Vue更新数组视图"
date:   2017-10-12 22:35:00
categories: Vue 前端
tags: Vue 前端 v-for
---

##问题描述：

在使用**v-for**循环渲染一个数组的时候，当我用js改变数组中的值，被绑定的视图不更新

vue官方文档中说明：由于 JavaScript 的限制，Vue 不能检测以下变动的数组：
当你利用索引直接设置一个项时，例如：```javascript vm.items[indexOfItem] = newValue ```
当你修改数组的长度时，例如：```javascript vm.items.length = newLength ```

为了解决第一类问题，以下两种方式都可以实现和```javascript vm.items[indexOfItem] = newValue ```相同的效果，同时也将触发状态更新：
```javascript
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)
// Array.prototype.splice
example1.items.splice(indexOfItem, 1, newValue)
为了解决第二类问题，你可以使用 splice：
example1.items.splice(newLength)
```

但是我的问题是v-for循环的是一个对象数组，我要改变的是数组中的一个对象,所以使用的方法是
只能把这一个数组项，单独抽出来，重新赋值，而不能单独改变数组项对象中的某一个值的值

错误的方式：
```javascript
items[index].signSelectedParam = false;
```

正确的方式：
```javascript
items[index].signSelectedParam = false     //改变数组某一项
Vue.set(items,index, items[index])         //重新赋值
```