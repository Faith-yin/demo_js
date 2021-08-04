<!--
 * @Date: 2021-06-12 16:30:13
 * @information: axios取消请求
-->
<template>
  <div>
    <com-02 ref="com02Ref"
            proProps="这是传过去的值哦~"
            @funCom02Emit="funCom02EmitPage17"></com-02>
  </div>
</template>

<script>
import axios from 'axios'

import Com02 from '@/components/Com02'

export default {
  components: {
    Com02
  },
  data () {
    return {
      url: `https://api.apiopen.top/getJoke?page=1&count=1&type=video`,
    }
  },
  methods: {
    fetchData () {
      let CancelToken = axios.CancelToken
      let source = CancelToken.source()
      // console.log(cancelToken, source)
      // console.log(axios.prototype)
      axios.get(this.url, {
        cancelToken: source.token
      }).then(res => {
        console.log('成功了', res)
      }).catch(err => {
        if (axios.isCancel(err)) {
          console.log('请求取消了')
        } else {
          console.log('失败了', err)
        }
      }).finally(() => {
        console.log('结束了')
      })

      source.cancel('不想请求了啊')

    },

    funCom02EmitPage17 (val) {
      console.log('funCom02EmitPage17-子组件响应的值：', val)
    },

  },
  created () {
    this.fetchData()
  },
}
</script>

<style lang="scss">
</style>
