<template>
  <div class="responsive_page_frame with_header main-container">

    <div class="responsive_page_content">

      <div class="responsive_page_template_content">

        <div class="no_header profile_page has_profile_background " :style="{ backgroundImage: `url('${$store.state.background}')` }">

          <div class="profile_header_bg">

            <div class="profile_header_bg_texture">

              <div class="profile_header">

                <div class="profile_header_content">

                  <div class="profile_header_centered_persona">
                    <div class="persona_name" style="font-size: 24px;">
                      <span class="actual_persona_name">{{ $store.state.user.screenName }}</span>
                    </div>
                  </div>

                  <div class="playerAvatar profile_header_size online">
                    <div class="playerAvatarAutoSizeInner"><img class="sapicAva" :src="$store.state.user.avatar"></div>
                  </div>

                  <div class="profile_header_badgeinfo">

                    <div class="profile_header_badgeinfo_badge_area">
                    </div>

                    <div class="profile_header_actions">
                    </div>
                  </div>

                  <div class="profile_header_summary">
                  </div>

                </div>
              </div>
            </div>
          </div>
          <div class="profile_content has_profile_background">

            <div class="profile_background_holder_content">
              <div class="profile_background_overlay_content"></div>
            </div>
            <div class="profile_content_inner">

              <div class="profile_leftcol">

                <div class="profile_customization_area">

                  <div class="profile_customization">
                    <div class="profile_customization_header">&nbsp;</div>

                    <div class="profile_customization_block">
                      <div class="screenshot_showcase">
                        <div class="screenshot_showcase_primary showcase_slot">
                          <div class="screenshot_showcase_screenshot">
                            <div class="profile_main_artbox" :style="{ 
                              backgroundImage: `url('${$store.state.background}')`,
                              width: `${$store.state.bgSize.w}px`,
                              height: `${$store.state.bgSize.h - 272}px`
                            }"> </div>
                            <!-- <img width="100%" style="max-width: 506px;" :src="$store.state.background"> -->
                          </div>
                          <div class="screenshot_showcase_itemname">
                          &nbsp;
                          </div>
                        </div>
                        <div class="screenshot_showcase_rightcol">
                          <div class="screenshot_showcase_smallscreenshot showcase_slot">
                            <div class="screenshot_showcase_screenshot">
                              <div class="profile_main_artbox_side1" :style="{ 
                                backgroundImage: `url('${$store.state.background}')`,
                                width: `${$store.state.bgSize.w}px`,
                                height: `${$store.state.bgSize.h - 272}px`
                              }"> </div>
                              <!-- <img width="100%" style="max-width: 100px;" :src="$store.state.background"> -->
                            </div>
                          </div>
                          <div class="screenshot_showcase_smallscreenshot screenshot_count">
                            <div class="screenshot_showcase_screenshot"> &nbsp;</div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bgPreloader" :style="{
      position: 'fixed',
      opacity: 0
    }">
      <img :src="background.steamUrl" v-for="background in nextBackgrounds" v-bind:key="background.url">
      <img :src="$store.state.background" ref="currentBgHolder" @load="imageUpdated">
    </div>

  </div>
</template>

<script>
export default {
  computed: {
    nextBackgrounds () {
      return this.$store.state.nextRandomBackgrounds
    }
  },
  methods: {
    imageUpdated () {
      if (this.$refs.currentBgHolder.naturalHeight && this.$refs.currentBgHolder.naturalWidth) {
        this.$store.commit('setBgSize', {
          w: this.$refs.currentBgHolder.naturalWidth,
          h: this.$refs.currentBgHolder.naturalHeight
        })
      }
    }
  }
}
</script>

<style scoped lang="stylus">
$color-1 = rgba(18, 21, 26, .9)
$color-3 = #8f98a0
$color-4 = #57cbde
$color-5 = rgba(83, 164, 196, 1)
$color-6 = rgba(69, 128, 151, 1)
$color-7 = #41778f
$color-8 = #3d697b
$color-9 = #262627
$color-10 = #000
$color-11 = #898989
$color-12 = #fff
$color-13 = #5491cf
$color-14 = #222223

.profile_main_artbox
    width 100%
    height 850px
    background-position -508px -271px

.profile_header_bg
    background $color-1
    opacity .9
    position relative
    max-width 1018px
    min-height 224px
    padding-bottom 16px
    margin 0 auto
    background-repeat no-repeat
    background-position center bottom

.profile_background_overlay_content
    background-color $color-1
    position absolute
    top 0
    right 0
    bottom 0
    left 0
    z-index 1

.profile_main_artbox_side1
    width 100%
    height 850px
    background-position -1022px -271px

.profile_customization
    background-color transparent
    position relative
    background-position top left
    background-repeat no-repeat
    border-radius 3px
    padding 0 10px 11px 10px
    margin-bottom 12px
    font-size 13px
    overflow hidden

.sapicAva
    border-radius 5px

.main-container
    flex 0 1 auto
    user-select none
    cursor default
    border-radius 0 0 10px 10px

div
    box-sizing content-box

    &.profile_page
        position relative
        min-width 950px
        background-image url('https://steamcommunity-a.akamaihd.net/public/images/profile/profile_bg.jpg')
        background-repeat repeat-x
        background-color $color-9

        &.has_profile_background
            background-color $color-10
            background-position center top
            background-repeat no-repeat

.responsive_page_frame
    color $color-3

.playerAvatar
    &.online
        background-color $color-4
        background linear-gradient( to bottom, $color-5 5%, $color-6 95%)
        filter none

        img
            background linear-gradient( to bottom, $color-7 5%, $color-8 95%)

    &.profile_header_size
        position relative
        width 166px
        height 166px
        border-radius 5px

        .playerAvatarAutoSizeInner
            position absolute
            top 2px
            right 2px
            bottom 2px
            left 2px

            img
                background none
                filter none
                display block
                padding 0
                width 100%
                height 100%

@media screen and (-webkit-min-device-pixel-ratio:0)
    div
        &.profile_page
            &.has_profile_background
                background-position 49.999% 0

.profile_header_bg_texture
    max-width 976px
    min-height 224px
    margin 0 auto
    background-repeat no-repeat
    background-position center

.profile_header
    position relative
    max-width 926px
    margin 0 auto
    padding-top 24px

    .playerAvatar
        &.profile_header_size
            float left
            margin-right 18px

    .persona_name
        line-height 40px
        font-size 24px
        color $color-12
        text-overflow ellipsis
        white-space nowrap
        overflow hidden
        font-family "Motiva Sans", Sans-serif
        font-weight 200

    .profile_header_centered_persona
        position absolute
        left 186px
        right 268px
        white-space nowrap

.profile_header_content
    position relative
    padding-top 8px
    color $color-11
    font-size 13px

.profile_header_summary
    overflow hidden
    padding-right 18px

.profile_header_badgeinfo
    float right

.profile_header_badgeinfo_badge_area
    width 268px

.profile_header_actions
    white-space nowrap

.profile_content
    position relative
    background-image url('https://steamcommunity-a.akamaihd.net/public/images/profile/profile_content_bg.png')
    background-position center
    background-repeat repeat-y
    padding 0 12px 64px 12px
    width 926px
    margin 0 auto
    font-size 13px

    &.has_profile_background
        background none
        overflow hidden

.profile_content_inner
    position relative

.profile_leftcol
    width 636px
    float left
    box-sizing initial

.profile_customization_header
    font-family "Motiva Sans", Sans-serif
    font-weight 200
    color $color-13
    font-size 20px
    line-height 30px
    overflow hidden
    white-space nowrap
    text-overflow ellipsis

.showcase_slot
    display block
    float left
    position relative

.screenshot_showcase_primary
    width 508px
    max-width 83%
    float left

    .screenshot_showcase_screenshot
        margin-bottom 4px

.screenshot_showcase_screenshot
    border 1px solid $color-10
    display block
    white-space nowrap
    overflow hidden

.screenshot_showcase_itemname
    word-wrap break-word

.screenshot_showcase_rightcol
    float right
    max-width 17%
    width 102px
    text-align center

.screenshot_showcase_smallscreenshot
    float none
    margin-bottom 11px

    &.screenshot_count
        display block
        height 57px
        line-height 57px
        background-color $color-14
        color $color-12

.profile_background_holder_content
    position absolute
    top 0
    right 0
    bottom 0
    left 0
    z-index 0
</style>

<style scoped src="@/assets/css/motiva_sans.css"></style>