<template>
  <div class="outer" >
    <h3>拖动下方滑块完成拼图</h3>
    <div class="img">
      <img 
        class="moveImg" 
        src="./images/nose.png" 
        alt=""
        :style="{top:data.top + 'px',left:data.left + 'px'}"
      >
    </div>
    <div class="move" ref="moveLine">
      <div 
        class="btn"
        @mousedown="btnMouseDown"
        :style="{left:data.left + 'px'}"
        >| | |</div>
    </div>
  </div>
</template>

<script setup>
  import { reactive , ref } from 'vue';
  const $props = defineProps({
    top:{
      type:Number,
      deafult:100 //89
    },
    left:{
      type:Number,
    }
  })
  const data = reactive({
    top:$props.top,
    left:10 ,//232,
    initMouseLeft:0,
    currentLeft:0,
    result:false
  })
  const moveLine = ref(null)
  const $emit = defineEmits(['result'])
  let btnMouseMove = (e) => {
    calBtnPosition(e.pageX,moveLine.value.offsetLeft)
    // 改变按钮位置
    data.left = data.currentLeft

  }
  let btnMouseDown = (e) => {
    // 鼠标点击时，给body绑定鼠标移动和离开的事件
    document.body.addEventListener('mousemove',btnMouseMove)
    document.body.addEventListener('mouseup',btnMouseUp)
    // 鼠标在btn点击的时候就要保存鼠标在btn中的距离
    data.initMouseLeft = e.offsetX; 
    console.log('down'); 
  }
  let btnMouseUp = () => {
    // 给页面绑定鼠标移动事件
    document.body.removeEventListener('mousemove',btnMouseMove)
    // 将结果给父组件
    if(Math.abs(data.left - $props.left)<=3){
      data.result = true
    }
    $emit('result',data.result)
    // 重置位置 和 结果
    data.left = 10
    data.result = false
    // 移除页面的鼠标松开事件
    document.body.removeEventListener('mouseup',btnMouseUp)
  }
  function calBtnPosition(a,b){
    // 移动位置 = 鼠标位置  - 滚动条离body的位置 - 鼠标离按钮的位置
    let left =  a  - b - data.initMouseLeft
    if(left <0) {
      left = 0
    }else if(left > 265){
      left = 265
    }
    // 判断按钮的位置是否超界
    data.currentLeft  = left
  }
</script>
<style lang="less" scoped>
.outer{
  width: 330px;
  // height: ;
  margin: 100px auto;
  text-align: center;
  border: 1px solid rgb(204, 196, 196);
  .img{
    position: relative;
    width: 311px;
    height: 155px;
    margin: 0 auto;
    background-image: url('./images/timg.jpg');
   .moveImg{
    position: absolute;
    left: 0;
    top: 0;
   }
  }
  .move{
    position: relative;
    width:311px ;
    margin: 20px 10px;
    height: 11px;
    background-color: #e5e4e5;
    border-radius: 3px;
    .btn{
      position: absolute;
      left: 0px;
      top: -5px;
      height: 23px;
      width: 46px;
      line-height: 20px;
      font-size: 10px;
      color: white;
      background-color: #1477ff;
      border-radius: 10px;
    }
  }
}
</style>