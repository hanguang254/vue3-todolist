<template>
  <div id="app">
    <!-- 绑定事件-->
    <MyHeader @receive="receive"></MyHeader>
    <MyList :todos="todos"></MyList>
    <MyFooterVue :todos="todos" @checkedAlltodo="checkedAlltodo" @clearAllTodo="clearAllTodo"></MyFooterVue>
  </div>
  
</template>

<script>
import MyHeader from "./components/MyHeader.vue"
import MyList from "./components/MyList.vue"
import MyFooterVue from "./components/MyFooter.vue"

export default {
  name: 'app',
  data(){
        return{
          //读取本地存储
            todos:JSON.parse(localStorage.getItem("todos")) || []
        }
        
    },
  components: {
    MyHeader,
    MyList,
    MyFooterVue,
  },
  methods: {
    receive(x){
       //接受Myheader的数据
       //存入data种
       this.todos.unshift(x)
    },
    //勾选or取消勾选 done值修改
    checktodo(id){
      this.todos.forEach((todos)=>{
        if(todos.id === id) todos.done = !todos.done
      })
    },
    //删除一个数据
    deletetodo(id){
      //filter数组过滤方法
      this.todos = this.todos.filter( todo => todo.id !== id)
    },
    //全选 与取消全选
    checkedAlltodo(done){
      this.todos.forEach((todo)=>{
        todo.done = done
      })
    },
    clearAllTodo(){
      this.todos = this.todos.filter((todo)=>{
        return !todo.done
      })
    }
  },
  watch:{
    todos:{
      //深度监视
      deep:true,
      // 执行任务
      handler(value){
        // 存储本地
        localStorage.setItem("todos",JSON.stringify(value))
      }
    }
    
    
    
  },
  //全局事件
  mounted(){
    this.$bus.$on('checktodo',this.checktodo)
    this.$bus.$on('deletetodo',this.deletetodo)
  },
  //解绑
  beforeDestroy(){
    this.$bus.$off('checktodo')
    this.$bus.$off('deletetodo')
  }
    
}
</script>

<style>
#app {
}
</style>
