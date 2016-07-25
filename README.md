# vue-search
### 一款基于 [vuejs](http://vuejs.org/) & [weui](http://weui.io/) 的全屏搜索组件


## 功能
* 根据配置的数据列表提供关键字`过滤搜索`功能
* 显示字段可配置


## 安装
npm install --save vue-search

## options
* show  组件显示条件
* items 待搜索的数据数组
* displaykey  显示对象的属性名称,默认`text`
* limit 最大显示条数,默认`5`
* label 搜索框标签提示文字,默认`搜索`
* inputholder 搜索框提示文字,默认`搜索`
* transtionModel 过渡动画切换模式,需要在CSS中实现对应的样式定义,默认实现`slide`

## 在你的vue项目中进行使用(with ES6)
```javascript
  import search from 'vue-search';
  export default {
     components:{
       	search
     },
     events:{
        	fullscreensearch:function(item){    //响应用户选择搜索项事件
        		console.log(item);
        		this.showSearch=false;
        	}
       }
  }
```

```html
    <search :show="showSearch" :items="items"></search>
```

