<template>
  <div>
    <imgCheck top="89" left="232" @result="imgCheckResult"></imgCheck>
  </div>
</template>

<script setup>
  // imgCheck组件
  import imgCheck from './components/imgCheck/index.vue'
  function imgCheckResult(result){
    if(result){
      alert("成功")
    }else{
      alert("失败")
    } 
  }
</script>

<style>
  *{  
	  -webkit-touch-callout:none;  /*系统默认菜单被禁用*/   
	  -webkit-user-select:none; /*webkit浏览器*/   
	  -khtml-user-select:none; /*早期浏览器*/   
	  -moz-user-select:none;/*火狐*/   
	  -ms-user-select:none; /*IE10*/   
	  user-select:none;   
    } 
  body{
   margin: 0 !important;
 }
</style>
