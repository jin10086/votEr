<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <img :style="{ opacity: $route.path === '/' ? 0 : 1 }" height="32" src="~@/assets/logo.png" class="logo" />
      </router-link>
      <Account />
    </nav>
    <router-view />
  </div>
</template>

<script>
import Account from '@/components/ui/Account'

export default {
  name: 'App',
  components: {
    Account,
  },
  created() {
    this.updateSize()
    addEventListener('resize', this.updateSize)
  },
  beforeDestroy() {
    removeEventListener('resize', this.updateSize)
  },
  methods: {
    updateSize() {
      const w = innerWidth
      let fs = 20
      if (w < 480) {
        fs = 12
      } else if (w < 1920) {
        fs = 12 + (w - 480) / 180
      }
      document.documentElement.style.fontSize = fs + 'px'
    },
  },
}
</script>

<style lang="stylus">
#app
  position relative

nav
  padding 24px 40px
  height 80px
  display flex
  justify-content space-between
  align-items center
  .logo
    display block
</style>
