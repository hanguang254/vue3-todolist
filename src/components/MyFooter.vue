<template>
    <div class="todo-footer" v-show="this.todos.length">
        <label>
            <input type="checkbox" :checked="isAll" @change="checkAll">
        </label>
        <span>
            <span>已完成 {{doneTotal}}</span> /全部完成{{todos.length}}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成</button>
    </div>
</template>

<script>

    export default {
        name:"MyFooter",
        props:["todos"],
        computed:{
            doneTotal(){
                //数组的reduce方法  pre元素开始值 
                // const x= this.todos.reduce((pre,current)=>{
                //     return pre + (current.done ? 1:0)
                // },0)
                // return x

                return this.todos.reduce((pre,current)=> pre +(current.done ? 1:0),0)
            },
            isAll(){
                return this.doneTotal === this.todos.length && this.todos.length > 0
            }
        },
        methods:{
            checkAll(e){
                this.$emit('checkedAlltodo',e.target.checked)
            },
            clearAll(){
                this.$emit('clearAllTodo')
            }
        }
    }
</script>

<style lang="css" scoped>

</style>