<template>
  <div>
    <Search/>
    <pagList></pagList>
  </div>
</template>

<script>
import Search from './components/Search.vue';
import pagList from './components/pagList.vue';

export default {
  name: 'App',
  components: {
    Search,
    pagList,
  }
}
</script>

