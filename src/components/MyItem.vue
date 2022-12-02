<template>
    <li>
        <label>
                                                    <!-- change事件 -->
            <input type="checkbox" :checked="msg.done" @change="handlechek(msg.id)">
            <span>{{msg.title}}</span>
        </label>
        <button class="btn btn-danger" @click="handledelete(msg.id)">删除</button>
        <button class="btn btn-danger">编辑</button>
    </li>
</template>

<script>
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
    background-color: brown;
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