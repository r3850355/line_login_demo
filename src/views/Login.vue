<template>
  <div class="home">
    <h1>Login Page</h1>
    <line-button @click="loginEvent()"></line-button>
  </div>
</template>

<script>
import LineButton from '@/components/LineButton'

export default {
  name: 'home',
  components: {
    LineButton
  },
  methods: {
    loginEvent() { // 當你按下按鈕發生的事件
        let URL = 'https://access.line.me/oauth2/v2.1/authorize?'
        // 必填
        URL += 'response_type=code' // 希望LINE回應什麼  但是目前只有code能選
        URL += `&client_id=${process.env.VUE_APP_LINE_CHANELL_ID}` // 你的頻道ID
        URL += `&redirect_uri=${process.env.VUE_APP_LINE_REDIRECT_URL}` // 要接收回傳訊息的網址
        URL += '&state=123456789' // 用來防止跨站請求的 之後回傳會傳回來給你驗證 通常設亂數 這邊就先放123456789
        URL += '&scope=openid%20profile' // 跟使用者要求的權限 目前就三個能選 openid profile email
        // 選填
        URL += '&nonce=helloWorld' // 順便將機器人也加好友
        URL += '&prompt=consent'
        URL += '&max_age=3600'
        URL += '&ui_locales=zh-TW'
        URL += '&bot_prompt=normal'
        window.open(URL, '_self') // 轉跳到該網址
    }
  }
}
</script>
