<template>
  <div class="cube-textarea-outer-wrapper">
    <div class="cube-textarea-inner-wrapper" :style="{width: width}" :class="{expanded: expanded}">
      <textarea
        class="cube-textarea"
        v-model="textareaValue"
        v-bind="$props"
        :placeholder="placeholder"
        :maxlength="maxlength"
        :disabled="disabled"
        @focus="handleFocus"
        @blur="handleBlur">
      </textarea>
      <span v-show="expanded" class="cube-textarea-indicator">{{remain}}</span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const COMPONENT_NAME = 'cube-textarea'
  const EVENT_INPUT = 'input'

  export default {
    name: COMPONENT_NAME,
    data() {
      return {
        textareaValue: this.value,
        expanded: false
      }
    },
    props: {
      value: {
        type: String,
        default: ''
      },
      cols: Number,
      rows: Number,
      readonly: Boolean,
      wrap: String,
      required: Boolean,
      placeholder: {
        type: String,
        default: 'please type here...'
      },
      dirname: String,
      form: String,
      name: String,
      autofocus: Boolean,
      disabled: {
        type: Boolean,
        default: false
      },
      maxlength: {
        type: Number,
        default: 60
      },
      width: {
        type: String,
        default: '274px'
      }
    },
    computed: {
      remain() {
        return this.maxlength - this.value.length
      }
    },
    watch: {
      value(newValue) {
        this.textareaValue = newValue
      },
      textareaValue(newValue) {
        this.$emit(EVENT_INPUT, newValue)
      }
    },
    methods: {
      handleFocus(e) {
        this.$emit('focus', e)
        this.expanded = true
      },
      handleBlur(e) {
        this.$emit('blur', e)
        if (this.textareaValue.length === 0) {
          this.expanded = false
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @require "../../common/stylus/variable.styl"

  .cube-textarea-outer-wrapper
    text-align: center
  .cube-textarea-inner-wrapper
    position: relative
    display: inline-block
    transition: height 200ms
    height: 34px
    &.expanded
      height: 74px
    textarea::-webkit-input-placeholder
      color: $color-light-grey-s !important
      text-overflow: ellipsis
  .cube-textarea-indicator
    position: absolute
    bottom: 7px
    right: 10px
    line-height: 20px
    color: $color-light-grey-s
    font-size: $fontsize-medium
  .cube-textarea
    width: 100%
    height: 100%
    text-align: left
    padding: 7px 10px
    resize: none
    box-sizing: border-box
    border-radius: 2px
    border: none
    color: $color-grey
    background-color: $color-background
    outline: none
    font-size: $fontsize-medium
    line-height: 20px
    &:focus
      outline: $textarea-outline-color solid 1px
      outline-offset: -1px
</style>
