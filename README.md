# javascript 设计模式

### 观察者模式
  
  #### 日常工作中的例子
  
  #### 1、比如监听 div 的 click Event , div.addEventListener('click',functuin(e){ ... }) ,观察 div 对象，当div被点击了，执行匿名函数
  
  #### 2、Vue  view-model 双向绑定，通过 Object.defineProperty 来实现对象的 ‘响应式’ ， reactiveGetter 进行依赖收集，reactiveSetter 更新属性时，通知观察者更新最新状态
  
  ```javascript
  // Subject --> save state 、notifyAllObserver when state change 
  class Subject {
    constructor() {
      this.state = 0 
      this.observers = []
    }
    
    getState() {
      return this.state
    }
    
    setState(state) {
      this.state = state 
      this.notifyAllObservers()
    }
    
    notifyAllObservers() {
      this.observers.forEach(observer => {
        observer.update()
      })
    }
    
    attach(observer) {
      this.observers.push(observer)
    }
  }
  
  // Observer 
  class Observer {
    constructor(name , subject) {
      this.name = name 
      this.subject = subject 
      this.subject.attach(this)
    }
    
    update() {
      console.log('${this.name}' update , state : ${this.subject.getState()}')
    }
  }
  
  // demo 
  let subject = new Subject() 
  let observer_1 = new Observer('observer_1',subject)
  let observer_2 = new Observer('observer_2',subject)
  
  // mock state change
  subject.setState(10086)
  
  
  ```
