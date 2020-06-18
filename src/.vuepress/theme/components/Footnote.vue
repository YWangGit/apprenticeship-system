<template>
  <footer class="theme-container footer">
    <span v-if="footerText">{{footerText}}</span>
  </footer>
</template>
<script>
export default {
  name: "Footnote",
  computed: {
    footerText() {
      return this.$site.themeConfig.footerText;
    }
  }
};
</script>
<style lang="stylus">
.theme-container.footer {
  margin-top: 20px;
  height: 70px;
  line-height: 70px;
  color: #4e6e8e;
  text-align: center;
  font-size: 20px;
  border-top: 1px solid #eaecef;
}
</style>
