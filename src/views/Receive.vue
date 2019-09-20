<template>
  <div class="about">
    <h1>Receive Page</h1>
    <h3>回傳回來的值：{{ query }}</h3>
    <hr>
    <h1>Token API</h1>
    <h3>回傳回來的值: {{ tokenResult }}</h3>
    <hr>
    <h1>IdToken Decode</h1>
    <h3>解析後的值: {{ idTokenDecode }}</h3>
    <hr>
    <router-link to="/">回登入頁</router-link>
  </div>
</template>

<script>
import axios from 'axios'
import Qs from 'qs'
import jwtDecode from 'jwt-decode'

export default {
  data () {
    return {
      query: {},
      tokenResult: {},
      idTokenDecode: {}
    }
  },
  mounted () {
    this.query = this.$route.query // 接網址的參數

    let options = Qs.stringify({ // POST的參數  用Qs是要轉成form-urlencoded 因為LINE不吃JSON格式
      grant_type: 'authorization_code',
      code: this.query.code,
      redirect_uri: process.env.VUE_APP_LINE_REDIRECT_URL,
      client_id: process.env.VUE_APP_LINE_CHANELL_ID,
      client_secret: process.env.VUE_APP_LINE_CHANELL_SECRET
    })

    axios.post('https://api.line.me/oauth2/v2.1/token', options, { headers: { 'Content-Type': 'application/x-www-form-urlencoded'}}).then(res => {
      this.tokenResult = res.data // 回傳的結果
      this.idTokenDecode = jwtDecode(res.data.id_token) // 把結果的id_token做解析
    })
    
  }
}
</script>

