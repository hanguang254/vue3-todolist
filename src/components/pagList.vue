<template>
    <div class="row">
        <!--展示用户列表-->
        <div v-show="info.users.length" class="card" v-for="user in info.users" :key="user.login">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url"   style='width: 100px'/>
            </a>
            <p class="card-text">{{ user.login }}</p>
        </div>
        <!---欢迎词-->
        <h1 v-show="info.isFirst">欢迎使用!</h1>
        <!--加载中--->
        <h1 v-show="info.isLoading">Loading...</h1>
        <!---错误信息-->
        <h1 v-show="info.errMsg">Something has been wrong, errorMessage: {{ info.errMsg }}</h1>
  </div>
</template>

<script>
    export default {
        name: 'pagList',
        data() {
            return {
                info:{
                    isFirst: true, //是否为第一次使用
                    isLoading: false, //是否在加载中
                    errMsg: '',
                    users:[],
                }
            }
        },
        mounted() {
            this.$bus.$on('getusers', (dataObj) => {
                // console.log("我收到数据",dataObj);
                //合并对象
                this.info = {...this.info,...dataObj}
            })
        },
    }
</script>

<style lang="css" scoped>
h1{
    text-align: center;
}
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}
.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}
.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}
.card-text {
  font-size: 85%;
}
</style>