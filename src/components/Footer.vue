<template>
  <footer class="footer">
    <p class="license" v-if="$siteConfig.license">
      All content under
      <a :href="$siteConfig.license.link">{{$siteConfig.license.text}}</a>
    </p>
    <p class="copyright">
      Powered by
      <a class="power" href="https://saber.land">Saber</a>, theme
      <a class="theme" href="https://github.com/geekplux/blog/tree/master/packages/saber-theme-paper">Paper</a>
    </p>
  </footer>
</template>

<style lang="scss" scoped>
@import '../styles/variables.scss';
footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 30px 0;
}

.license {
  font-size: 12px;
  color: $gray;

  a {
    color: #000;
  }
}

.copyright {
  font-size: 12px;
  color: $gray-light;

  a {
    color: $gray;
  }
}
</style>


<script>
export default {}
</script>
