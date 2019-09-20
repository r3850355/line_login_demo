<template>
  <img
    :src="buttonStatus"
    @mouseover="hoverEvent()"
    @mousedown="pressEvent()"
    @mouseup="hoverEvent()"
    @mouseleave="initEvent()"
    @click="$emit('click')"
  >
</template>

<script>
export default {
  data () {
    return {
      buttonStatus: require('../assets/images/btn_login_base.png')
    }
  },
  methods: {
    hoverEvent () {
      this.buttonStatus = require('../assets/images/btn_login_hover.png')
    },
    initEvent () {
      this.buttonStatus = require('../assets/images/btn_login_base.png')
    },
    pressEvent () {
      this.buttonStatus = require('../assets/images/btn_login_press.png')
    }
  }
}
</script>

