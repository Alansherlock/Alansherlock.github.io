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
function mapObj(list) {
    var obj = {};
    for (let item of list) {
        console.log(!obj[item.id]);
        if (!obj[item.id]) {
            console.log(item.id);
            obj[item.id] = item.list;
        }
        else {
            obj[item.id] = obj[item.id].concat(item.list);
            console.log(obj[item.id]);
        }
    }
    return Object.keys(obj).map(key => {
        return {
            id: key,
            list: obj[key]
        }
    });
}
</script>
</body>
</html>
```