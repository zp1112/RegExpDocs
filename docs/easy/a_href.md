## 给全页面中的所有a标签的href属性的值后面加一个随机数

```js
const pat = new RegExp('<a.+?href=\"(.+?)\".*>.+<\/a>', 'g');
document.bosy.innerHTML.replace(pat, function(result, $1) {
  return $1 + Math.random();
})
```

### 解释

```js
const pat = new RegExp('<a.+?href=\"(.+?)\".*>.+<\/a>', 'g');

//  <a.+?表示匹配<a后面跟着一个活多个任意字符的非贪婪匹配
// .*表示匹配0个火多个人员字符的贪婪匹配
// .+表示a标签里面匹配非空的人员字符
```