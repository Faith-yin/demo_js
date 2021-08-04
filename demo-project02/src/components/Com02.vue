<!--
 * @Date: 2021-07-24 11:36:48
 * @information: 
-->
<template>
  <div id="com02">
    <div>{{userProvide1}}</div>

    <slot name="slot1"></slot>
    <slot name="slot2"
          :obj="com02Obj"></slot>

    <button @click="onModify">更改provide中的值</button>

  </div>
</template>

<script>
export default {
  props: {
    proProps: {
      type: String,
      default: '默认值'
    }
  },
  inject: {
    userProvide1: {
      default: () => {
        return '这是默认值吧1'
      }
    }
  },
  data () {
    return {
      com02Name: 'com02',
      com02Obj: { name: 'ypf', age: 18 }
    }
  },
  computed: {
    com02Age () {
      return 18
    }
  },
  watch: {
    com02Name () {
      return 'boy'
    }
  },
  created () {

  },
  mounted () {
    console.log('com02:', this)

    let fun = this._events.funCom02Emit[0]
    fun('这就是响应的值啊')
  },
  activated () {

  },
  methods: {
    funCom02 () {
      const val = 'yyy'
      this.$emit('funCom02Emit', val)
    },

    funCom0201 () {
      const val = 'fff'
      this.$emit('funComEmit0201', val)
    },

    onModify () {
      this.userProvide1 = 'yyyyyy'
      this.$nextTick(() => {
        console.log(111, this.userProvide1)
      })
    },


  }
}
</script>

<style lang="scss">
</style>