<template>
  <label for="" class="input__body" :class="{'error' : error}">
    <p class="input__text">{{ label }}</p>
    <input
      class="input"
      :type="type"
      :placeholder="placeholder"
      :value="value"
      @input="onInput($event)"
    >
    <p class="input__error" v-if="error">{{ error }}</p>
    <svg class="input__error-img" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" v-if="error">
      <g clip-path="url(#clip0_211_5977)">
        <path d="M8.00004 5.33334V8M8.00004 10.6667H8.00671M14.6667 8C14.6667 11.6819 11.6819 14.6667 8.00004 14.6667C4.31814 14.6667 1.33337 11.6819 1.33337 8C1.33337 4.3181 4.31814 1.33334 8.00004 1.33334C11.6819 1.33334 14.6667 4.3181 14.6667 8Z" stroke="#F04438" stroke-width="1.33333" stroke-linecap="round" stroke-linejoin="round"/>
      </g>
      <defs>
        <clipPath id="clip0_211_5977">
          <rect width="16" height="16" fill="white"/>
        </clipPath>
      </defs>
    </svg>

  </label>
</template>

<script>
export default {
  name: "input",
  props: ['label', 'type', 'placeholder', 'error', 'value'],
  methods: {
    onInput(e) {
      this.$emit('input', e.target.value)
      this.$emit('onInput')
    }
  }
}
</script>

<style scoped lang="scss">
.input__body {
  width: 100%;
  &.error {
    position: relative;
    .input {
      border-color: #F04438;
      padding-right: 38px;
    }
    .input__error-img {
      position: absolute;
      right: 8px;
      top: 40px;
    }
  }
  .input {
    padding: 10px 14px;
    width: 100%;
    background: #FFFFFF;
    border: 1px solid #D0D5DD;
    box-shadow: 0px 1px 2px rgba(16, 24, 40, 0.05);
    border-radius: 8px;
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;
    color: #101828;
    &::placeholder {
      color: #98A2B3;
    }
  }
  .input__text {
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
    color: #344054;
    margin-bottom: 6px;
  }
  .input__error {
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    color: #F04438;
    margin-top: 6px;
  }
}
</style>
