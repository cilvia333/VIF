<template lang="pug">
header
  .container
    .menu-button(@click="buttonClick" :class="{ 'menu-button_open': isActiveHamburger }")
        .menu-icon
    nav.header-nav(:class="{ 'nav_open': isActiveHamburger }")
      ul.header-menu
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#eyecatch'" to="/") TOP
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#news'" to="/") NEWS
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#lineup'" to="/") LINE UP
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#timetable'" to="/") TIME TABLE
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#attention'" to="/") ATTENTION
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#access'" to="/") ACCESS
        li: nuxt-action-link.header-link(@click="navClick" v-scroll-to="'#contact'" to="/") CONTACT
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import { store } from '~/store/index'

@Component({
  components: {
    NuxtActionLink: () => import('../utils/ NuxtActionLink.vue')
  }
})
export default class Header extends Vue {
  get isActiveHamburger(): Boolean {
    return store.getters['menu/isActiveHamburger']
  }

  buttonClick() {
    store.dispatch('menu/changeHamburgerState', !this.isActiveHamburger)
  }

  navClick() {
    store.dispatch('menu/changeHamburgerState', false)
  }
}
</script>

<style lang="sass" scoped>
header
  width: 100vw
  height: 60px
  position: fixed
  top: 0
  left: 0
  background-color: rgba($white, 0)
  z-index: 300

.container
  width: 100%
  height: 100%
  display: flex
  @include screen-mq(md)
    justify-content: flex-end
    align-items: center

  & > *
    padding-top: 0
    padding-bottom: 0

.header-nav
  width: 100%
  height: 100%
  padding-left: 0

  @include screen-mq(md)
    position: absolute
    background-color: $white
    top: 0px
    right: 0px
    width: 100%
    min-height: 100vh
    padding: 0
    left: 0
    z-index: 299
    text-align: center
    transform-origin: left top
    transform: translateY(-100%)
    transition: all 0.3s cubic-bezier(0, 1.06, 0.54, 1)
    overflow: hidden

  &.nav_open
    @include screen-mq(md)
      transform: translateY(0%)

  ul
    display: flex
    margin: 0 0 0 auto
    padding: 0
    max-width: 300px
    height: 100%
    align-items: center
    justify-content: space-between
    text-align: left

    @include screen-mq(md)
      display: inline-flex
      margin: 0
      padding: 100px 0
      width: 90%
      flex-direction: column
      align-items: flex-end
      justify-content: space-between

    li
      display: block
      margin-right: 5px
      text-align: center

      @include screen-mq(md)
        display: inline
        text-align: center

.header-menu
  li
    &:nth-child(1)
      margin-bottom: 30px
      position: relative
      .header-link
        color: $black !important
      &::after
        content: ""
        position: absolute
        bottom: -20px
        left: 0
        width: 150%
        height: 3px
        background-color: $black
    &:nth-child(3n)
      .header-link
        color: $theme-cyan

    &:nth-child(3n+1)
      .header-link
        color: $theme-magenta

    &:nth-child(3n+2)
      .header-link
        color: $theme-yellow

  .header-link
    position: relative
    display: inline-block
    font-size: 16px
    padding: 0 5px

    color: black
    background-color: $white

    transition: all 0.5s cubic-bezier(0, 1.06, 0.54, 1)

    &:hover
      color: red
      &::after
        width: 100%
        width: calc(100% + 1px)

    @include screen-mq(md)
      display: block
      font-size: 50px

    @include screen-mq(sm)
      font-size: 40px

//Menu Button

.menu-button
  padding-left: 0

  width: 30px
  height: 30px
  background-color: transparent
  border: none
  outline: none
  cursor: pointer
  transition: 0.2s cubic-bezier(0.17, 0.07, 0.02, 0.98)
  z-index: 301

  display: none

  @include screen-mq(md)
    display: flex;

  &:hover
    transform: scale(0.9)

  .menu-icon
    margin: 16px auto
    width: 25px
    height: 2px
    background-color: $black
    position: relative
    border-radius: 4px
    transition: 0.5s cubic-bezier(0.17, 0.07, 0.02, 0.98)
    &::before
      content: ''
      position: absolute
      top: -8px
      left: 0
      width: 25px
      height: 2px
      background-color: $black
      border-radius: 4px
      transition: 0.5s cubic-bezier(0.17, 0.07, 0.02, 0.98)

    &::after
      content: ''
      position: absolute
      bottom: -8px
      left: 0
      width: 25px
      height: 2px
      background-color: $black
      border-radius: 4px
      transition: 0.5s cubic-bezier(0.17, 0.07, 0.02, 0.98)

.menu-button_open
  .menu-icon
    width: ((30px - 4px) * sqrt(2)) + 4px
    transform: rotate(-135deg)
    &::before
      top: -1 * (30px - 4px )/2 / sqrt(2)
      left: (30px - 4px)/2 / sqrt(2)
      width: (30px - 4px)/2 / sqrt(2) + 4px
      transform: rotate(90deg)
    &::after
      bottom:  -1 * (30px - 4px )/2 / sqrt(2)
      left: (30px - 4px)/2 / sqrt(2)
      width: ((30px - 4px)/2 / sqrt(2)) + 4px
      transform: rotate(90deg)
</style>
