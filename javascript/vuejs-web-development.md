# [Vue.js前端开发](https://book.douban.com/subject/26994869/)

## 基础特性

### 实例和选项

模板

```
<div id="app">
  <p>123</p>
</div>
<script id="tpl" type="x-template">
  <div class='tpl'>
    <p>This is a tpl from script tag</p>
  </div>
</script>
<script type="text/javascript">
 var vm = new Vue({
    el: '#app'
    template: '#tpl'
});
```

数据

```
var data = { a: 1}
var vm = new Vue({
  data: data
})
```

方法

```
<button v-on:click="alert">alert</button>
new Vue({
  el: '#app',
  data: {a: 1},
  methods: {
    alert: function() {
      alert(this.a);
    }
  }
});
```

生命周期

```
var MyView = Vue.component('myView', {
  template : '<div><p>{{a}}</p><button @click="destroy()"/><input v-model="a" /></div>',
  data : function() {
    return {
      a : 1
    }
  },
  methods : {
    destroy : function() {
      this.$destroy();
    }
  },
  beforeCreate: function() {
    console.log('beforeCreate');
  },
  created: function() {
    console.log('created');
  },
  beforeMount: function() {
    console.log('beforeMount');
  },
  compiled: function() {
    console.log('compiled');
  },
  activated: function() {
    console.log('activated', document.getElementById('app').innerHTML);
  },
  deactivated: function() {
    console.log('deactivated');
  },
  beforeDestroy: function() {
    console.log('beforeDestroy');
  },
  destroyed: function() {
    console.log('destroyed');
  },
  mounted: function() {
    console.log('mounted');
    // this.$destroy();
  },
  beforeUpdate: function(argu) {
    console.log('beforeUpdate', document.getElementById('app').innerHTML);
  },
  updated: function(argu) {
    console.log('updated', document.getElementById('app').innerHTML);
  }
     	});

new Vue({
  el : '#app'
})
```

### 数据绑定

绑定语法

```
<span>Hello {{ * name }}</span>
<div v-bind:id="'id-' + id"></div>
{{ name.split('').join(':')
{{ name | uppercase }}
<image v-bind:src="avatar" />
```

表单控件

```
<input type="text" v-model="message" />
<span>Your input is : {{ message }}</span>
<label><input type="radio" value="male" v-model="gender">男</lable>
<label><input type="radio" value="female" v-model="gender">女</lable>
<input type="checkbox" v-model="checked"  value="123"/>
<span>checked : {{ checked }}</span>
<select v-model="selected">
  <option selected>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selected: {{ selected }}</span>
```

模板渲染

