<template>
    <transition appear
        name="animate__animated animate__bounce"
        enter-active-class="animate__bounceIn"
        leave-active-class="animate__bounceOut"
    >
        <li>
            <label>
                                                        <!-- change事件 -->
                <input type="checkbox" :checked="msg.done" @change="handlechek(msg.id)">
                <span v-show="!msg.isEdit">{{msg.title}}</span>
                <!-- blur失去焦点 -->
                <input type="text" 
                v-show="msg.isEdit"  
                :value="msg.title"
                @blur="handleblur(msg,$event)"  
                ref="inputedit"
                >
            </label>
            <button class="btn btn-danger" @click="handledelete(msg.id)">删除</button>
            <button v-show="!msg.isEdit" class="btn btn-edit" @click="handleEdit(msg)">编辑</button>
        </li>
    </transition>
</template>

<script>
import 'animate.css';

    export default {
        name:"MyItem",
        props:["msg"],
        methods: {
            handlechek(id){
                this.$bus.$emit('checktodo',id)
            },
            handledelete(id){
                if(confirm("确认删除吗？")){
                    this.$bus.$emit('deletetodo',id)
                }
            },
            //编辑功能
            handleEdit(msg){
                //判断msg是否存在isedit
                //APi  hasOwnProperty判断对象是否存在一个属性
                if(Object.hasOwnProperty.call(msg,'isEdit')){
                    msg.isEdit = true
                }else{

                    this.$set(msg,"isEdit",true)
                }
                //自动获取焦点
                this.$nextTick(function(){
                    this.$refs.inputedit.focus()
                })    
            },
            // 失去焦点
            handleblur(msg,e){
                msg.isEdit = false
                this.$bus.$emit('updatatodo',msg.id,e.target.value)
            }
        },
    }
</script>

<style lang="css" scoped>
li{
    list-style-type: none;
    height: 20px;
    margin-left: -40px;
    height: 25px;
}
li button{
    display: none;
    float: right;
}
/* hover鼠标悬浮 */
li:hover {
    background-color: aqua;
}
li:hover button{
    display: block;
}

</style>