<template>
    <ul class="todo-main">
        <MyItem v-for="tobj in todos" 
            :key="tobj.id" 
            :msg="tobj" >
        </MyItem>
    </ul>
</template>

<script>
import MyItem from "./MyItem.vue"

export default {
    name:"MyList",
    components:{MyItem},
    props:["todos"],
}
</script>

<style lang="css" scoped>

</style>