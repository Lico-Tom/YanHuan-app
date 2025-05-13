<!--
web-view 是一个 web 浏览器组件，可以用来承载网页的容器，会自动铺满整个页面。
开发一个套壳App，把下面<web-view></web-view>组件里src的网址链接替换成你想要的链接就可以了。
需要注意的是，如果是做套壳小程序，各小程序平台，web-view 加载的 url 需要在后台配置域名白名单，包括内部再次 iframe 内嵌的其他 url 。
-->
<template>
  <view v-if="isConnected">
    <web-view src="http://192.168.31.248:8123"></web-view>
  </view>
  <view v-else>
    <form @submit.prevent="checkBackendConnection">
      <div>
        <label for="username">ip:</label>
        <input type="text" id="ip" v-model="loginForm.ip" required>
      </div>
      <div>
        <label for="password">port:</label>
        <input type="password" id="port" v-model="loginForm.port" required>
      </div>
      <button type="submit">确定</button>
    </form>
  </view>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      loginForm: {
        ip: "192.168.31.248",
        port: "8123"
      },
      msg: "msg",
      url: "http://192.168.31.248:8123",
      isConnected: true
    }
  },
  onLoad() {
  },
  methods: {
    checkBackendConnection() {
      axios.get(this.url).then(response => {
        this.isConnected = true
      })
    }
  }
}
</script>

<style lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg: #283443;
$light_gray: #fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
  }
}

/* reset element-ui css */
.login-container {
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;

    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
  }

  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
}
</style>

<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;

  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 160px 35px 0;
    margin: 0 auto;
    overflow: hidden;
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
    }
  }

  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }

  .thirdparty-button {
    position: absolute;
    right: 0;
    bottom: 6px;
  }

  @media only screen and (max-width: 470px) {
    .thirdparty-button {
      display: none;
    }
  }
}
</style>
