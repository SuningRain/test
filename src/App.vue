<template>
  <div id="app">
    <ListDetail :data="testList"></ListDetail>
  </div>
</template>

<script>
import ListDetail from './components/ListDetail.vue'

export default {
  name: 'App',
  data () {
    return {
      testList: [
        { title: '标题一', detail: '标题一详情' },
        { title: '标题二', detail: '标题二详情' },
        { title: '标题三', detail: '标题三详情' },
        { title: '标题四', detail: '标题四详情' }
      ]
    }
  },
  components: {
    ListDetail
  }
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
}
</style>
