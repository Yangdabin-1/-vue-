# Vue2

# Vue3

----

## 滑动拼图解锁

*初始*

>组件需要传入碎片图和完整图和位置参数（left/top）
>
><img src="C:\Users\Yangdabin-1\AppData\Roaming\Typora\typora-user-images\image-20221219202437369.png" alt="image-20221219202437369" style="zoom: 67%;" />

*布局*

>子绝父相

*逻辑*

>点击按钮，并移动鼠标，按钮和碎片会左右移动
>
>- 需要鼠标的三个事件 ====> 点击 ， 移动 ， 松开
>
>- mousedown
>  - 事件给滑块绑定
>- mousemove
>  - 事件给body绑定 
>  - 若绑在按钮身上，则只会在按钮内移动鼠标才会触发 ； 需要鼠标移除按钮时，也可以移动滑块
>  - 解除时机 ===>   mouseup事件触发时
>- mouseup
>  - 事件给body绑定 ， mousemove触发时触发
>  - 解绑时机 ====> mouseup触发时 ， 自己解绑自己

*位置计算*

>滑块位置 = 鼠标的位置 - 滚动条的位置 - 鼠标距离滑块的位置
>
>鼠标的位置
>
>- 鼠标距离body的位置
>
>- event.pageX ===> event是鼠标移动事件
>
>滚动条的位置
>
>- 滚动条距离body的位置
>- 滚动条Node.offserLeft
>
>鼠标距离滑块的位置
>
>- event.offsetX ===> event是鼠标点击事件（即点击滑块时）

*结果*

>根据组件收到的props ===> top , left
>
>- 判断left是否与鼠标位置的距离在误差内
>
>- 组合式API  ====> defineProps()
>
>- ```js
>    const $props = defineProps({
>      top:{
>        type:Number,
>        deafult:100 //89
>      },
>      left:{
>        type:Number,
>      }
>    })
>  ```
>
>- 
>
>将判断结果通过自定义事件传送给父组件
>
>- 自定义事件API : defineEmits(['A','B'])
>
>- ```js
>  //父组件
>  <imgCheck top="89" left="232" @result="imgCheckResult"></imgCheck>>
>  function imgCheckResult(result){  }
>  
>  //子组件
>  const $emit = defineEmits('result') //接收自定义事件
>  $emit('result',result) //触发自定义事件 + 通信
>  ```
>
>- 
>
>

----
