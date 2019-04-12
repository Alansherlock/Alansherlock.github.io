---
title: canvas水印
tag: canvas
---
上次写了canvas水印现在整理下，方便下次需要拿取出来使用，也可以供封装为组件

##canvas水印

``` html
<template>
    <div id="watermark">
        <canvas id="canvas" height='100%' width='100%'>
            你的浏览器不支持canvas,请升级你的浏览器
        </canvas>
        <canvas id="repeat-watermark" height='100%' width='100%'>
            你的浏览器不支持canvas,请升级你的浏览器
        </canvas>
    </div>
</template>
<script>
export default {
    data() {
        return {

        }
    },
    component: {

    },
    async mounted() {
        await this.loadWatermark();
        await this.getWatermark();
    },
    methods:{
        // 先制作小水印
        loadWatermark() {
            let canvas = document.getElementById('canvas');
            if (!canvas.getContext) return;
            // 小画布的宽高
            canvas.height = 100;
            canvas.width = 100;
            let ctx = canvas.getContext('2d');
            ctx.clearRect(0,0,160,100);  //绘制之前画布清除
            ctx.font="20px 黑体";  
            ctx.rotate(-20*Math.PI/180);
            ctx.fillStyle = "rgba(100,100,100,0.1)";
            ctx.fillText("刘泽浩", -20, 80);
            ctx.rotate('20*Math.PI/180');  //坐标系还原
        },
        getWatermark() {
            // 平铺满整个容器
            let crw = document.getElementById('repeat-watermark');
            let canvas = document.getElementById('canvas');
            if (!crw.getContext) return;
            // 整个容器的宽高
            let height = document.getElementById('watermark').offsetHeight;
            let width= document.getElementById('watermark').offsetWidth;
            crw.width = width;
            crw.height = height;
            let ctxr = crw.getContext("2d");
            ctxr.clearRect(0,0,crw.width,crw.height);  //清除整个画布 \
            //主要是这个API
            let pat = ctxr.createPattern(canvas, "repeat");    //在指定的方向上重复指定的元素  
            ctxr.fillStyle = pat;  
            ctxr.fillRect(0, 0, crw.width, crw.height);
        }
    },
}
</script>
<style lang="scss" scoped>
#watermark {
    position: relative;
    width: 100%;
    height: 100%;
}
#repeat-watermark{
    position:absolute;
    top:0;
    z-index:10;
    background: #fff;
}
</style>

```
emmm