# Hold-Shift-and-Check-Checkboxes
<a href="https://xl-z4869.github.io/Hold-Shift-and-Check-Checkboxes/index.html">效果：点击+shift之后中间会都被选中</a>
<p>这是一个JS 实现 Checkbox 中按住 Shift 的多选功能</p>
 
 
### 一、知识点
#### 1.数组和querySelectorAll
用querySelectorAll得到的数组是伪数组，可以使用forEach，但没有数组的一些方法，例如push,pop,splice等，需要用Array.from()将其转化成真数组
 ```
const inputs=Array.from(document.querySelectorAll('input[type="checkbox"]'))
 ```

#### 2.用slice来得到第一个选择和第二个选择之间的所有队列
slice(start,end,'x','y')是从下标为start的开始截取，到下标为end的结束，之间可以插入x,y等若干元素，同时返回被截取的数值，因此利用这一特点，获得连个点击之间的队列
```
inputs.slice(lastCheck,newCheck)
```

#### 3.通过Math.min和Math.max来判断大小
获得两个点击数列的下标之后，需要明白，后点击的下标不一定就大，先点击的也不一定就小，因此用slice时，同时也要进行两者之间的比较
```
inputs.slice(Math.min(lastCheck),Math.max(newCheck))
```

### 二、主要步骤
#### 1.获得所有input元素，同时为每个input设置监听事件
```
const inputs=Array.from(document.querySelectorAll('input[type="checkbox"]'))
inputs.forEach(input => {
  input.addEventListener('click', clickHandler);
})
```

#### 2.判断是否被选中，并获得第一的点击的下标
```
let lastCheck=null
if(input.checked){     //input是指inputs中的一个
  lastCheck=inputs.indexOf(this)
}
```

#### 3.再次判断，这一次判断lastCheck有没有同时也要判断shift是否被按中，获得第二个下标
```
if(lastCheck!==null&&e.shiftKey){
  let newCHeck=inputs.indexOf(this)
}
```

#### 4.获得两个下标之后，获得下标之间的队列，是他们全部被选中
```
inputs.slice(Math.min(lastCheck),Math.max(newCheck)).forEach(input=>{
  input.checked = true
})
```
