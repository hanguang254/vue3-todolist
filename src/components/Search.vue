<template>
    <section class="jumbotron">
        <h3 class="jumbotron-heading">查询Github账号</h3>
        <div>
        <input type="text" placeholder="输入账号" v-model="keyword"/>&nbsp;
        <button @click="searchUsers">Search</button>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

    export default {
        name: 'SearchInput',
        data() {
            return {
                keyword: '',
            }
        },
        methods: {
            searchUsers() {
                axios.get(`https://api.github.com/search/users?q=${this.keyword}`).then(
                    response => {
                        // console.log(response.data.items);
                        this.$bus.$emit('getusers', response.data.items);
                    },
                    error => {
                        console.log("请求失败！",error.message);
                    }
                )
            }
        },
    }
</script>

<style lang="css" scoped>
section{
    text-align: center;
}
</style>