<template lang="pug">
  .menu__window
    .menu__window-buttons
      .menu__window-button.menu__window-button-download(@click="$store.dispatch('downloadZip')")
        .menu__window-button-text Download ZIP

      .menu__window-shadow

      .menu__window-button(@click="$store.dispatch('randomBackground')")
        .menu__window-button-text Random BG
      
      .menu__window-button(@click="$store.dispatch('getCurrentBg')")
        .menu__window-button-text Get this BG

      .menu__window-section-container
        
      input.menu__window-button.textbox.noclick#urltextbox(placeholder="Paste a background URL here", v-model="bgURL")

      .menu__window-item-discord(@click="$store.dispatch('openDiscord')")
          img.menu__window-discord(
            src="https://discordapp.com/api/guilds/304986224467378177/widget.png?style=banner2"
          )

      .menu__window-section-container

        .menu__window-button.noclick.small
          .menu__window-button-text Zoom Scale:

        .menu__window-scale__container
          input.menu__window-scale__input(
            name="scale"
            type="radio"
            value="50"
            v-model="previewScale"
            id="scale50"
          )
          label(for="scale50").menu__window-scale__label
            .menu__window-scale__button 50%

          input.menu__window-scale__input(
            name="scale"
            type="radio"
            value="75"
            v-model="previewScale"
            id="scale75"
          )
          label(for="scale75").menu__window-scale__label 
            .menu__window-scale__button 75%

          input.menu__window-scale__input(
            name="scale"
            type="radio"
            value="100"
            v-model="previewScale"
            id="scale100"
          ) 
          label(for="scale100").menu__window-scale__label
            .menu__window-scale__button 100%

          input.menu__window-scale__input(
            name="scale"
            type="radio"
            value="125"
            v-model="previewScale"
            id="scale125"
          )
          label(for="scale125").menu__window-scale__label
            .menu__window-scale__button 125%
    .menu__window-credits
      .menu__window-credits-text Made with ❤️ by TrueCarry and The Oddball

</template>

<script>
export default {
  computed: {
    previewScale: {
      get () {
        return this.$store.state.previewScale
      },
      set (value) {
        this.$store.commit('setPreviewScale', value)
      }
    },
    bgURL: {
      set (value) {
        if (value.match(/\.(?:jpeg|jpg|png)$/i)) {
          this.$store.commit('setBackgroundURL', value)
        }
      },
      get () {
      }
    }
  }
}
</script>

<style scoped lang="stylus">
$color-1 = #12151a
$color-2 = #000
$color-3 = #08090b
$color-4 = #1c2129
$color-5 = #fff
$color-6 = rgba(0,0,0,0.4)
$color-7 = #36bbf7
$color-8 = #702df9
$color-9 = #272d38

.menu__window
    height 100%
    width 250px
    background $color-1
    flex-shrink 0
    user-select none
    display flex
    flex-direction column
    align-items center

.menu__window-section-container
    margin-top 10px

.menu__window-discord
    margin 10px 10px 0 10px
    transition filter 0.25s ease
    text-align center
    display flex
    cursor pointer
    height 55px
    border-radius 3px

    &:hover
        filter drop-shadow(0px 3px 10px $color-2)
        transition filter 0.25s ease

.menu__window-button
    background-color $color-3
    transition background-color 0.25s ease
    border-radius 3px
    cursor pointer
    margin 10px 10px 0 10px
    text-align center
    display flex
    align-items center
    justify-content center

    &:hover
        transition background-color 0.25s ease
        background-color $color-4

    &.noclick
        cursor default
        filter initial
        background-color $color-3

    &.textbox
        cursor text
        width 232px
        height 30px
        color $color-5
        border none
        outline none
        padding 6px
        text-align center
        transition box-shadow 0.25s ease-in-out

        &:focus
            box-shadow 0 0 40px $color-6

    &.small
        .menu__window-button-text
            margin 4px
            font-size 14px

.menu__window-button-text
    bottom 11px
    font-size 17px
    font-weight 300
    color $color-5
    margin 15px 0

.menu__window-button-download
    background linear-gradient(45deg, $color-7 0%, $color-8 100%)
    position relative
    z-index 2
    opacity 0.8
    transition opacity 0.25s ease

    &:hover
        opacity 1
        transition opacity 0.25s ease

.menu__window-shadow
    background linear-gradient(45deg, $color-7 0%, $color-8 100%)
    filter blur(12px)
    position relative
    height 53px
    top -63px
    margin 10px 10px -63px 10px
    width 232px

.menu__window-item
    transition background-color 0.25s ease
    cursor pointer
    margin 10px 10px 0 10px
    text-align center
    transition filter 0.25s ease
    display flex
    align-items center
    justify-content center

    &:hover
        transition filter 0.25s ease
        filter drop-shadow(0px 3px 10px $color-2)
        transition background-color 0.25s ease
        background-color $color-4

.menu__window-item-text
    bottom 11px
    color $color-5
    margin 0

.menu__window-scale__container
    display flex
    flex-direction row
    flex-wrap wrap
    justify-content space-between
    padding 0 10px

.menu__window-scale__input
    display none

    &:checked
        +label
            background $color-9
            cursor default

.menu__window-scale__label
    transition all 0.25s ease
    background-color $color-3
    border-radius 3px
    cursor pointer
    margin-top 5px
    text-align center
    width 49%
    flex 0 0 auto
    padding 12px

    &:hover
        background $color-4

.menu__window-scale__button
    bottom 11px
    text-shadow 0px 4px 10px $color-2
    color $color-5

.menu__window-credits
    position absolute
    bottom 0

.menu__window-credits-text
    color $color-5
    font-size 11px
    margin-bottom 5px

*
    box-sizing border-box

</style>
