<!--
 * @Date: 2021-07-03 19:43:11
 * @information: cookie用法
-->

<template>
  <div id="page18">
    <form>
      <input type="text"
             v-model="namePage18">
      <input type="text"
             v-model="vauePage18">
    </form>

    <button @click="set">设置cookie</button>
    <button @click="get">获取cookie</button>
    <button @click="del">删除cookie</button>

    <com-02 ref="com02Ref"
            proProps="这是传过去的值哦~"
            @funCom02Emit="funCom02EmitPage18"
            @funComEmit0201="funCom0201EmitPage18">
      <div slot="slot1">
        <div>slot1-这是插槽的内容啊</div>
        <div>开森啊</div>
      </div>

      <template slot="slot2"
                slot-scope="data">
        <div>
          slot2-这是插槽的内容啊 - {{ JSON.stringify(data) }}
        </div>
      </template>
    </com-02>

  </div>
</template>

<script>
import CookieUtil from '@/assets/js/util/cookie.js'

import mixins01 from '@/mixins/mixins01'

import Com02 from '@/components/Com02'

export default {
  mixins: [mixins01],
  provide () {
    return {
      userProvide1: 'ypf1'
    }
  },
  components: {
    Com02
  },
  data () {
    return {
      namePage18: '',
      vauePage18: '',

      proj01: 'proj01_value',

      objPage18: {
        a: {
          b: {
            c: 111
          }
        }
      },
    }
  },
  computed: {
    computedPage18 () {
      return 'start-' + this.proj01
    }
  },
  watch: {
    proj01 (newVal, oldVal) {
      console.log('watch 监听到了', newVal)
    }
  },
  created () {

  },
  mounted () {
    console.log('page18:', this)

    setTimeout(() => {
      this._render()
    }, 5000);

  },
  activated () {

  },
  methods: {
    set () {
      CookieUtil.setCookie(this.namePage18, this.vauePage18, 1 * 24 * 60 * 60 * 1000)
      alert('已设置')
    },

    get () {
      let val = CookieUtil.getCookie(this.namePage18)
      alert(val)
    },

    del () {
      CookieUtil.removeCookie(this.namePage18)
      alert('已删除')
    },

    funCom02EmitPage18 (val) {
      console.log('funCom02EmitPage18-子组件响应的值：', val)
    },

    funCom0201EmitPage18 (val) {
      console.log('funCom0201EmitPage18-子组件响应的值：', val)
    },




  },
}
</script>

<style lang="scss">
</style>