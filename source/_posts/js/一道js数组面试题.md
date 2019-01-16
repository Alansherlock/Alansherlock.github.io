---
title: 一道数组面试题
tag: JavaScript
---
# 我们来爬一爬
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<script>
// old
let oldlist = [
    {id:1,list:[1,2,3]},
    {id:2,list:[4,5]},
    {id:1,list:[4,5]}
];
let keys = Array.from(new Set(oldlist.map(item => item.id)))
let newlist= keys.map(key=>{
    var temp = new Array();
      oldlist.filter(item=>item.id==key).reduce((pre,cur)=>{
        temp = temp.concat(cur.list)
    },0)
    return {id:key,list:temp}
})
console.log(JSON.stringify(newlist));
</script>
</body>
</html>
```