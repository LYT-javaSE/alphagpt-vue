<template>
  <div class="aui-wrapper aui-page__login">
    <div class="aui-content__wrapper">
      <main class="aui-content">
        <div class="login-header">
          <h2 class="login-brand">{{ $t('brand.lg') }}</h2>
        </div>

        <login-username></login-username>
<!--        <login-email></login-email>-->

        <div class="login-footer">
          <p>
            <a href="http://demo.open.renren.io/renren-security" target="_blank">{{ $t('login.demo') }}</a>
          </p>
          <p><a href="https://www.renren.io/" target="_blank">{{ $t('login.copyright') }}</a>2022 © renren.io</p>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import LoginUsername from './zhangzhiyu/login-username'
import LoginEmail from './zhangzhiyu/login-email'
export default {
    components: { LoginUsername, LoginEmail },
}
</script>
