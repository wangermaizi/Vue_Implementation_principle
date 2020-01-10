# Vue_Implementation_principle
简单描述了Vue的实现原理

### 定义一个class 类 Vue

### 在构造constructor传入一个option对象参数

#### 这个option参数配置这个类的所有参数,包括data,methods等

### 通过选择器获取挂载的DOM对象

#### 在这个操作的过程中,在挂载前可以执行挂载前执行的生命周期函数,beforeMount(),挂载后亦是如此

### 将传入的option参数,托管到这个类的$options属性上

### 设置观察者模式的事件队列对象$watchEvent

### 定义一个类方法ProxyData(),用于数据代理,代理原理是defineproperty中的set()方法和get()方法

#### 在ProxyData()中,循环所有的$options.data(毕竟是代理数据,总要先拿到数据先)

##### 在循环中设置Object.defineProperty(this,key,{set(v){return this.$options.data[key] = v},get(){return this.$options.data[key]}})

### 定义一个类方法observe()用于劫持事件,并进行事件的监听

#### 在observe()方法中,依旧是循环$options.data的内容

##### 在循环中设置Object.defineProperty(this.$options.data,key,{set(v){value = v,if (that.$watchEvent[key]) {that.$watchEvent[key].forEach(function (item,index) {item.update()}})}}}

