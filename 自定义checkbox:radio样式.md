

# 问题

UI给的checkbox设计图是这样的：
![uiCheckbox](https://i.imgur.com/zrubm1w.png)
但是浏览器默认是这样的：
![defaultCheckbox](https://i.imgur.com/Ktrc7Hf.png)
也太丑了吧，相差有点远！明显跟整个页面风格不协调。


# 实现
在网上搜寻了一下，找到了实现原理，采用以下几个css技术，即可轻松实现自定义的checkbox/radio的效果：

1. label标签for属性。原生的input是不能够改变浏览器默认的样式的，只能通过隐藏input，改变label的样式来模拟checkbox/radio；但是如何实现点击label标签能够达到勾选/去勾选的input的效果呢，答案就是label的for属性。label的for属性值设置成和input的id相同时，当点击label时和直接点击input效果相同。
2. 伪类选择器:checked, 当checkbox/radio被选中时input会加上checked这个伪类，可以通过这个为选中后的checkbox/radio设置不同的样式
3. +相邻兄弟选择器，表示选择该元素后面的兄弟节点。



## 自定义checkbox样式

样例代码：[在线预览地址](https://jsrun.net/RhXKp)

```html
<style>
.checkbox-name {
  vertical-align: middle;
  font-size: 16px
}

.checkbox-beauty {
  width: 16px;
  height: 16px;
  line-height: 16px;
  text-align: center;
  border: 1px solid #D9D9D9;
  display: inline-block;
  margin: 0 15px 0 3px;
  vertical-align: middle;
}

input[type="checkbox"]:checked + .checkbox-beauty::after {
  display: inline-block;
  width: 16px;
  height: 16px;
  content: '✓';
  font-size: 16px;
  font-weight: normal;
  background-color: #4EBD74;
  color: #ffffff!important;
}
</style>
<div>
  <span class="checkbox-name">前端</span>
  <input type="checkbox" name="checkboxName" value="123" id="checkboxName1" hidden/>
  <label for="checkboxName1" class="checkbox-beauty"></label>
</div>
```



## 自定义radio样式

样例代码，[在线预览地址](https://jsrun.net/uhXKp)

```html
<style>
input[type=radio]:checked + .radio-beauty {
  background-clip: content-box;
  padding: 3px;
  background-color: #4EBD74;
  border-color: #4EBD74
}

.radio-beauty {
  box-sizing: border-box;
  display: inline-block;
  width: 16px;
  height: 16px;
  background: #ffffff;
  border: 1px solid #D9D9D9;
  border-radius: 50%;
  vertical-align: middle;
}

.radio-name {
  vertical-align: middle;
  font-size: 14px;
}
</style>
<div>
  <input id="shape1" name="box-shape" type="radio" value="123" hidden/>
  <label for="shape1" class="radio-beauty">
  </label>
  <span class="radio-name">
    前端
  </span>
</div>
```



> 参考：https://github.com/jawil/blog/issues/29
