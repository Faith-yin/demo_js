<!--
 * @Date: 2021-07-03 19:43:11

  1. cookie用法
  2. vue源码学习时的一些测试代码
  3. vue文件中的样式优先级 > 公共样式文件的优先级
     !important 属性的样式优先级 > 内联样式优先级

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

    <div style="margin: 30px 0">----------------------------------分割线--------------------------------------</div>

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

    <div style="margin: 30px 0">----------------------------------分割线--------------------------------------</div>

    <div class="test-css_container">
      <div class="text">element: 当table使用fixed时，表中的自定义组件将呈现两次，然后重复调用接口</div>
      <div id="text_1"
           style="marign-top: 10px">这是一些测试文件</div>
    </div>

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
.test-css_container {
  padding: 20px;
  border: 1px solid #1fb19e;

  .text {
    font-size: 20px;
    color: #ff6700;
  }

  #text_1 {
    margin-top: 100px !important;
    color: #1fb19e;
  }
}
</style>