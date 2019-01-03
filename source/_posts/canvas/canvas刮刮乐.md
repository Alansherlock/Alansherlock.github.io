---
title: canvas刮刮乐
tag: canvas
---
上次写了canvas刮刮乐现在整理下，方便下次需要拿取出来使用，也可以供封装为组件

``` html
<template>
<div class="guaguale">
    <p>一等奖</p>
    <canvas 
    id="canvas"
    width="500"
    height="1000"
    @mousedown="down"
    @mouseup="up"
    @mousemove="move"
    >
    您的浏览器不支持canvas！
    </canvas>
</div>
</template>
<script>
export default {
    data() {
        return {
            flag:false,
            lx:'',
            ly:''
        }
    },
    mounted() {
        this.guagua();
    },
    methods:{
        guagua() {
            let cv = document.getElementById("canvas"),
            p = document.getElementsByTagName("p")[0];
            //设置中奖几率
            let num = 10000 * Math.random(),
                result = "";
            if (num < 1000) {
                // result = "三等奖";
            }
            if (num < 50) {
                // result = "二等奖";
            }
            if (num < 5) {
                // result = "一等奖";
            }
            p.innerText = result;
            try {
                let ct = cv.getContext("2d");
                //绘制背景色
                ct.fillStyle = "skyblue";
                ct.fillRect(0, 0, 500, 1000);
                //设置绘制状态
                ct.lineCap = "round";　　 //设置线条两端为圆弧
                ct.lineJoin = "round";　　 //设置线条转折为圆弧
                ct.lineWidth = 60;
                /*设置新绘制清除新绘制内容和原内容的重叠区域*/
                ct.globalCompositeOperation = "destination-out";
            } catch (e) {
                console.log(e);
            }
        },
        down(e) {
            this.flag = true;
            this.lx = e.offsetX;
            this.ly = e.offsetY;
        },
        up() {
            this.flag = false;
        },
        move(e) {
            if (this.flag) {
                let cv = document.getElementById("canvas");
                let ct = cv.getContext("2d");
                ct.beginPath();
                ct.moveTo(this.lx, this.ly);
                ct.lineTo(e.offsetX, e.offsetY);
                ct.stroke();
                ct.closePath();

                //更新坐标
                this.lx = e.offsetX;
                this.ly = e.offsetY;
            }
        }
    }
}
</script>
<style lang="scss" scoped>
    #canvas {
        /* canvas 默认宽高 300*150 
        css设置的宽高，只能设置canvas对象在页面显示的大小。
        并不能增加画布内部的像素数
        */
        border: 1px solid black;
        /* width: 500px;
        height: 500px; */
        margin: 0 auto;
        position: absolute;
        left: 0;
        top: 0;
    }

    .guaguale {
        width: 500px;
        height: 500px;
        background: url("../../assets/dou.png") no-repeat;
        background-size: 100% 100%;
        position: relative;
    }

    .guaguale p {
        font-size: 50px;
        line-height: 500px;
        text-align: center;
        width: 100%;
    }
</style>

```