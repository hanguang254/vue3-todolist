<template>
    <div class="ftx">
        <!-- //键盘事件 -->
        <input type="text" placeholder="请输入事件，回车键确认" @keyup.enter="add">
    </div>
</template>

<script>
import {nanoid} from "nanoid"

    export default {
        name:"MyHeader",
        methods: {
            add(e){
                // 判断不能为空输入
                if(!e.target.value) return alert("输入不能为空")
                // 将输入值封装为一个对象
                //nanoid 生成一个随机序列号
                const obj = {id:nanoid(),title:e.target.value,done:false}
                //将数据给receive方法传递给我APP
                this.$emit('receive',obj)
                //清空输入框
                e.target.value = ""
        },
    }
}
</script>

<style lang="css" scoped>
/* .ftx input{
    text-align: center;
} */
input{
    
}
</style>