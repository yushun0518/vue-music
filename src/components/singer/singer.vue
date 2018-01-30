<template>
  <div>
    页面
  </div>
</template>

<script type="text/ecmascript-6">
  import {getSingerList} from 'api/singer'
  import {ERR_OK} from 'api/config'

  const HOT_SINGER_LEN = 10
  const HOT_NAME = '热门'

  export default {
    data() {
      return {
        signers: []
      }
    },
    created() {
      this._getSignerList()
      // this._normalizeSinger(this.singers)
      setTimeout(() => {
        this._normalizeSinger(this.singers)
      }, 2000)
    },
    methods: {
      _getSignerList() {
        getSingerList().then((res) => {
          if (res.code === ERR_OK) {
            this.singers = res.data.list
            // console.log(this.singers)
          }
        })
      },
      _normalizeSinger(list) {
        let map = {
          hot: {
            title: HOT_NAME,
            items: []
          }
        }
        list.forEach((item, index) => {
          if (index < HOT_SINGER_LEN) {
            map.hot.items.push({
              id: item.Fsinger_id,
              name: item.Fsinger_name,
              avatar: `https://y.gtimg.cn/music/photo_new/T001R150x150M0000025NhlN2yWrP4.jpg?max_age=2592000`
            })
          }
        })
        console.log(map)
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  .singer
    position: fixed
    top: 88px
    bottom: 0px
    width: 100%
</style>
