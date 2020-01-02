### Computed计算属性  

#### Computed的第一个作用（计算）

>Computed的初衷是用于简单运算的，在模板中放入太多的逻辑会让模板过重且难以维护。例如：
>```
><div id="example">
>  {{ message.split('').reverse().join('') }}
></div>
>
>```
>在这里，模板不是简单的逻辑申明，而变成了复杂的变量操作。当你想在模板中多次引用的时候，就会更加难以处理。所以，对于任何复杂逻辑，你都应当使用`计算属性`。

```
<div id="example">
  {{ message}}
</div>
var vm = new Vue({
    el: '#example',
    data: {
        message: 'Hello'
    },
    computed:{
        //getter
        reversedMessage:function(){
            return this.message.split('').reverse().join('');
        }
  }
```  

### Computed的第二个作用（监听）
1.Computed用来监控自己定义的变量，该变量不在data里面声明，直接在Computed里面定义，然后就可以在页面上进行双向数据绑定展示出结果或者用作其他处理  

2.Computed比较适合对多个变量或者对象进行处理后返回一个结果值，也就是`多个变量中的某一个值发生了变化则我们监控的这个值也就会发生变化`，举例：购物车里面的商品列表和总金额之间的关系，只要商品列表里面的商品数量发生变化，或减少或增多或删除商品，总金额都应该发生变化。这里的这个总金额使用Computed属性来进行计算是最好的选择 

在开发公众号的时候。遇到一个具体的场景。访客入园有时间段的选择。  

* 默认情况：`起始时间`按照当前时间计算，`终止时间`不能小于`起始时间`
* 当选择了起始时间：`起始时间`变化，`终止时间`随着变化且不能小于`起始时间`
* 先选择`终止时间`：`起始时间`的最大时间不能超过终止时间

```
<mt-datetime-picker class="datec"
            ref="pickerStartTime" 
            type="datetime" 
            year-format="{value} 年"
            month-format="{value} 月"
            date-format="{value} 日"
            hour-format="{value} 时"
            v-model="pickerValueStartTime"
            @confirm="this.handleConfirmStartTime"
            @cancel="this.closeStartdate"
            :startDate="startDate"
            :endDate="endDate"
            show=true>
        </mt-datetime-picker>
        <mt-datetime-picker class="datec"
            ref="pickerEndTime" 
            type="datetime" 
            year-format="{value} 年"
            month-format="{value} 月"
            date-format="{value} 日"
            hour-format="{value} 时"
            v-model="pickerValueEndTime"
            @confirm="this.handleConfirmEndTime"
            @cancel="this.closeEnddate"
            :startDate="startDateOver"
            show=true>
</mt-datetime-picker>



 computed: {
        //起始时间的最小时间
        startDate:{
            get(){
                return new Date();
            },
            set(newvalue){
                
            }
        },
        //终止时间的最小时间
        startDateOver:{
            get(){
                //对应第二三种判断
                if(this.chooseStartTime){
                    return this.chooseStartTime
                }else{
                    return new Date();
                }
            },
            //因为选择了终止日期后,数据会发生变化、监视当前属性值的变化，当属性值发生变化时执行，更新相关的属性数据
            set(newvalue){
                return new Date(newvalue);
            }
        },
        //起始时间的最大时间
        endDate:{
            get(){
                //对应第二三种情况监听选择了结束时间，起始时间的最大值就要变化
                if(this.pickerValueEndTime){
                    return this.pickerValueEndTime
                }else{

                }
            },
            set(){
            }
        },
    },

```  

---

### 计算属性缓存 vs 方法
你可能已经注意到我们可以通过在表达式中调用方法来达到同样的效果：
```
<p>Reversed message: "{{ reversedMessage() }}"</p>
```

```
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}

```
我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，`不同的是计算属性是基于它们的响应式依赖进行缓存的`。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。这也同样意味着下面的计算属性将不再更新，因为 Date.now() 不是响应式依赖：
```
computed: {
  now: function () {
    return Date.now()
  }
}
```

参考文档 ： https://cn.vuejs.org/v2/guide/computed.html