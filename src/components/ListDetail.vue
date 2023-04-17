<template>
  <div class="list-detail">
    <div class="left-list-wrap">
      <div
        :class="{
          'left-list': true,
          'left-list__active': curItemDetail === item.detail
        }"
        v-for="(item, index) in showList"
        :key="index"
        @click="setDetail(item)">
        <span>{{ item.title }}</span>
      </div>
    </div>
    <div class="right-detail-wrap">
      <div class="right-detail" v-if="curItemDetail">
        <span class="right-detail-content">{{ curItemDetail }}</span>
        <button @click="hideItem">点击隐藏</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      curItem: null,
      curIndex: -1,
      needHideList: [],
      showList: []
    }
  },

  computed: {
    curItemDetail () {
      const { curItem } = this
      return curItem && curItem.detail
    }
  },

  mounted () {
    this.initFirstItem()
  },

  methods: {
    initFirstItem () {
      if (this.data && this.data.length) {
        this.showList = [...this.data]
        this.curItem = this.data[0]
        this.curIndex = 0
      }
    },
    setDetail (item) {
      this.curItem = item
    },
    hideItem () {
      this.needHideList.push(this.curItem.title)
      this.changeCurItem()
    },
    changeCurItem () {
      const { showList, curItem, data, needHideList } = this
      let curIndex = showList.findIndex(item => item.title === curItem.title)
      this.showList = data.filter((item) => {
        return needHideList.indexOf(item.title) === -1
      })
      this.curIndex = Math.min(curIndex, this.showList.length - 1)
      this.curItem = this.showList[this.curIndex]
    }
  }
}

</script>
<style lang='scss' scoped>
.list-detail {
  height: 100vh;
  box-sizing: border-box;
  padding: 20px;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  .left-list-wrap {
    box-sizing: border-box;
    width: 120px;
    height: 100%;
    padding: 0 10px;
    border-right: 1px solid #ccc;
    .left-list {
      margin-bottom: 20px;
      padding: 10px;
      cursor: pointer;
      background-color: paleturquoise;
      &__active {
        background-color: rgb(133, 172, 212);
      }
    }
  }
  .right-detail-wrap {
    box-sizing: border-box;
    height: 100%;
    padding-left: 20px;
    flex: 1;
    .right-detail {
      height: 100%;
      display: flex;
      flex-direction: column;
      &-content {
        flex: 1;
      }
    }
  }
}
</style>