<template>
  <div>
    <Menu mode="horizontal" theme="light">
      <a
        href="https://qiita.com/advent-calendar/2019/nuxt-js"
        target="_blank"
        rel="noopener noreferrer"
      >
        <MenuItem class="brand" name="">
          <logo />
          Nuxt.js Advent Calendar 2019 for Qiita
        </MenuItem>
      </a>

      <a
        href="https://www.iviewui.com/"
        target="_blank"
        rel="noopener noreferrer"
      >
        <MenuItem name="">
          Made with iView
        </MenuItem>
      </a>
    </Menu>
    <nuxt />
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
export default {
  components: {
    Logo
  }
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.ivu-menu {
  display: flex;
  justify-content: space-between;
  padding: 0 5%;
}

.brand {
  display: flex;
}
</style>
