## 我们在使用已定义好的组件的时候可以传入属性
   1. 我们可以在组件的内容获取到传进来的值  this.props.attr
   2. 我们不能在组件内部更改属性值
   3. this.props.children 获取组件的子元素
   
## javascript
   1.arr.map(function(a,b,c){
        a:每一个值
        b:下标
        c:原数组
   })
   
## 渲染的组件必须是唯一的，返回的组件必须只有一个根元素

## react特性
   1. 单项数据流
   2. 虚拟dom  （加快程序运行效率）
   4. 组件化开发
   
##  组件中添加事件 bind();
    
    this指针会发生改变：<div onClick={this.change.bind(this)}> 
    
## 关键字
    
    state   children  
        
## this.state   内部改变组件状态

    this.state 设置
    this.setstate()重新渲染
    
## 外部传入通过 props