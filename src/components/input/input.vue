<template>
  <div class="cube-input-wrapper">
    <div class="cube-input-clear" v-if="_showClear" @click="handleClear">
      <slot>
        <i class="cubeic-wrong"></i>
      </slot>
    </div>
    <input
      ref="input"
      v-model="inputValue"
      v-bind="$props"
      :type="type"
      :disabled="disabled"
      :readonly="readonly"
      :autocomplete="autocomplete"
      :autofocus="autofocus"
      @focus="handleFocus"
      @blur="handleBlur"
    >
  </div>
</template>

<script type="text/ecmascript-6">
  const COMPONENT_NAME = 'cube-input'
  const EVENT_INPUT = 'input'
  const EVENT_BLUR = 'blur'
  const EVENT_FOCUS = 'focus'

  export default {
    name: COMPONENT_NAME,
    data() {
      return {
        inputValue: this.value
      }
    },
    props: {
      value: [String, Number],
      type: {
        type: String,
        default: 'text'
      },
      disabled: {
        type: Boolean,
        default: false
      },
      placeholder: String,
      readonly: {
        type: Boolean,
        default: false
      },
      autofocus: {
        type: Boolean,
        default: false
      },
      autocomplete: {
        type: Boolean,
        default: false
      },
      name: String,
      id: String,
      form: String,
      minlength: Number,
      maxlength: Number,
      resize: String,
      min: Number,
      max: Number,
      step: Number,
      tabindex: String,
      clearable: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      _showClear() {
        return this.clearable && this.inputValue && !this.readonly && !this.disabled
      }
    },
    watch: {
      value(newValue) {
        this.inputValue = newValue
      },
      inputValue(newValue) {
        this.$emit(EVENT_INPUT, newValue)
      }
    },
    methods: {
      handleFocus(e) {
        this.$emit(EVENT_FOCUS, e)
      },
      handleBlur(e) {
        this.$emit(EVENT_BLUR, e)
      },
      handleClear(e) {
        this.inputValue = ''
        this.$refs.input.focus()
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
    @require "../../common/stylus/variable.styl"
    .cube-input-wrapper
      position: relative
      font-size: $fontsize-large
      line-height: 1
      color: $input-font-color
      background-color: $input-bgc
      input
        width: 100%
        padding: 10px
        box-sizing: border-box
        color: inherit
        line-height: inherit
        outline: none
        &:focus
          outline: $input-outline-color solid 1px
          outline-offset: -1px
    .cube-input-clear
      position: absolute
      right: 0
      top: 0
      bottom: 0
      width: 1em
      height: 1em
      padding: 10px 8px
      margin: auto
      color: $input-clear-icon-color
      + input
        padding-right: 32px
</style>
