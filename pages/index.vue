<template>
  <div class="login">
      <div action="" class="login__item login__item-left">
        <form class="login__form" @submit.prevent>
          <svg class="login__logo" width="49" height="36" viewBox="0 0 49 36" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M19.5035 11.7837L15.7315 7.95905C13.1876 10.5273 11.6111 14.0804 11.6111 18.0007C11.6111 21.9213 13.1907 25.4661 15.7315 28.0462L19.5035 24.2164C18.5471 23.2447 17.8095 22.0454 17.3793 20.7085H31.622C31.1918 22.0454 30.4542 23.2447 29.4947 24.2164L33.2698 28.0462C35.8156 25.4661 37.3867 21.9213 37.3867 18.0007C37.3867 14.0804 35.8156 10.5273 33.2698 7.95905L29.4947 11.7837C30.4542 12.7551 31.1918 13.9567 31.622 15.2932H17.3793C17.8095 13.9567 18.5471 12.7551 19.5035 11.7837Z" fill="#101828"/>
            <path d="M37.3477 3.82626C40.9372 7.45826 43.1538 12.4719 43.1538 18.0006C43.1538 23.5293 40.9372 28.5449 37.3477 32.167L41.122 36C45.6813 31.386 48.5 25.0204 48.5 18.0006C48.5 10.9796 45.6813 4.61522 41.122 0L37.3477 3.82626ZM11.6492 3.82626L7.87447 0C3.32185 4.61522 0.5 10.9796 0.5 18.0006C0.5 25.0204 3.32185 31.386 7.87447 36L11.6559 32.1737C8.0663 28.5449 5.84617 23.5293 5.84617 18.0006C5.84617 12.4735 8.0663 7.45826 11.6492 3.82626Z" fill="#101828"/>
          </svg>
          <h1 class="login__title">Log in to your account</h1>
          <div class="login__inputs">
            <AppInput
              v-for="(input, i) in form"
              v-model.trim="input.value"
              :key="i"
              :label="input.label"
              :type="input.type"
              :placeholder="input.placeholder"
              :error="input.error"
              @onInput="onInputCheck"
            />
          </div>
          <div class="login__forgot">
            <div class="login__checkbox_body" @click="rememberChecked = !rememberChecked">
              <div class="login__checkbox" :class="{'active' : rememberChecked}"></div>
              <p class="login__checkbox_text">Remember me</p>
            </div>
            <nuxt-link to="/" class="login__link">Forgot password</nuxt-link>
          </div>
          <button class="login__btn" @click="submitForm">Sign in</button>
          <p class="login__support">Can’t log in to your account? <nuxt-link to="/" class="login__link">Ask support</nuxt-link></p>
        </form>
      </div>
    <div class="login__item login__item-right"></div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      haveChecked: false,
      rememberChecked: false,
      form: [
        {
          label: 'Email',
          type: 'email',
          placeholder: 'name@hoteldomain.com',
          value: '',
          error: '',
        },
        {
          label: 'Password',
          type: 'password',
          placeholder: '••••••••',
          value: '',
          error: ''
        }
      ]
    }
  },
  methods: {
    checkForm() {
      const regex =  new RegExp('^[^\\s@]+@([^\\s@.,]+\\.)+[^\\s@.,]{2,}$')
      this.form[0].error =  !regex.test(this.form[0].value) ? 'Please check email address' : ''
      this.form[1].error = !this.form[1].value ? 'Please fill in your password' : ''
    },
    submitForm() {
      this.checkForm()
      this.haveChecked = true
    },
    onInputCheck() {
      this.haveChecked ? this.checkForm() : false
    }
  }
}
</script>


<style lang="scss" scoped>
.login {
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}
.login__item-right {
  background-image: url("@/assets/img/login-bg.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  @media (max-width: 768px) {
    display: none;
  }
}
.login__item-left {
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.login__inputs {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-bottom: 24px;
}

.login__form {
  max-width: 360px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.login__logo {
  width: 46px;
  height: 36px;
}

.login__title {
  margin: 24px 0 32px 0;
  text-align: center;
}

.login__forgot {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 8px;
  .login__link {
    margin-left: auto;
  }
}

.login__checkbox_body {
  cursor: pointer;
  display: flex;
  gap: 8px;
  align-items: center;
}

.login__checkbox {
  cursor: pointer;
  width: 16px;
  height: 16px;
  background: #FFFFFF;
  border: 1px solid #D0D5DD;
  border-radius: 4px;
  transition: .3s;
  &.active {
    background: #F9F5FF;
    position: relative;
    &:before {
      position: absolute;
      content: url("@/assets/img/checked-mark.svg");
      top: 1px;
      left: 1px;
      margin: auto;
    }
  }
}

.login__checkbox_text {
  font-weight: 500;
  font-size: 14px;
  line-height: 20px;
  color: #344054;
}

.login__link {
  font-weight: 600;
  font-size: 14px;
  line-height: 20px;
  color: #6941C6;
}

.login__btn {
  padding: 10px 18px;
  background: #7F56D9;
  border-radius: 8px;
  width: 100%;
  font-weight: 600;
  font-size: 16px;
  line-height: 24px;
  color: #FFFFFF;
  text-align: center;
  margin: 24px 0 32px;
}

.login__support {
}

.login__item-right {
}
</style>
