<template>
  <section class="titlebar">
    <div class="resizeHandle resizeHandleTop"></div>
    <div class="resizeHandle resizeHandleLeft"></div>
    <img class="titlelogo" src="@/assets/images/logo.png">
    <span class="titletext"> Steam.Design</span>
    <div class="actionbuttons">
      <button class="minimizebutton actionbutton" @click="minimize"><svg aria-hidden="true" version="1.1" width="10" height="10"><path d="M 0,5 10,5 10,6 0,6 Z"></path></svg></button>
      <button class="maxmimizebutton actionbutton" @click="maximize">
        <svg :class="isMax ? 'hidden' : ''" aria-hidden="true" version="1.1" width="10" height="10" v-if="!isMax">
          <path d="M 0,0 0,10 10,10 10,0 Z M 1,1 9,1 9,9 1,9 Z"></path>
        </svg>
        <svg :class="isMax ? '' : 'hidden'" aria-hidden="true" version="1.1" width="10" height="10" v-else>
          <path d="m 2,1e-5 0,2 -2,0 0,8 8,0 0,-2 2,0 0,-8 z m 1,1 6,0 0,6 -1,0 0,-5 -5,0 z m -2,2 6,0 0,6 -6,0 z"></path>
        </svg>
      </button>
      <button class="closebutton actionbutton" @click="close">
        <svg aria-hidden="true" version="1.1" width="10" height="10">
          <path d="M 0,0 0,0.7 4.3,5 0,9.3 0,10 0.7,10 5,5.7 9.3,10 10,10 10,9.3 5.7,5 10,0.7 10,0 9.3,0 5,4.3 0.7,0 Z"></path>
        </svg>
      </button>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    close () {
      this.curWindow.close()
    },
    maximize () {
      if (!this.isMax) {
        this.curWindow.maximize()
      } else if (this.isMax) {
        this.curWindow.unmaximize()
      }
    },
    minimize () {
      this.curWindow.minimize()
    }
  },
  computed: {
    curWindow () {
      return this.$store.state.currWindow
    },
    isMax () {
      return this.$store.state.isMaximized // pbbl wont work
    }
  }
}
</script>

<style scoped lang="stylus">
$color-1 = #12151a
$color-2 = #07080a
$color-3 = #5f6873
$color-4 = #f04747
$color-5 = #fff

.titlebar 
  height 40px
  -webkit-app-region drag
  background-color #12151A
  user-select none

.actionbuttons
    float right
    position relative
    width 135px
    height 31px
    background-color $color-2

.actionbutton
    height 31px
    width 45px
    position relative
    background none
    margin-right -4px
    border none
    outline none
    fill #ffffff
    filter drop-shadow( 0px 3px 2px black)
    transition background-color 0.25s ease

    &:hover
        transition background-color 0.25s ease
        background-color $color-3

.closebutton
    &:hover
        transition background-color 0.25s ease
        background-color $color-4

.titlelogo
    height 25px
    width 25px
    position relative
    top 7px
    left 7px

.resizeHandle
    position absolute
    top 0px
    left 0px
    app-region no-drag

    &.resizeHandleTop
        width 100%
        height 5px

    &.resizeHandleLeft
        width 3px
        height 28px

.titletext
    color $color-5
    position relative
    bottom -1px
    left 9px
    font-weight 100
    font-size 20px

</style>
