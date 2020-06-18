<template>
  <header class="header">
    <el-carousel  :interval="5000" arrow="always" height="400px">
      <el-carousel-item v-for="(item, index) in imgList" :key="index">
        <img alt="Vue logo" :src="$withBase(item)" class="carousel-img" />
      </el-carousel-item>
    </el-carousel>
    <h2 class="app-title" v-if="logoImg">
      <img :src="$withBase(logoImg)"  class="app-logo" />
    </h2>
  </header>
</template>
<script>
export default {
  name: "Header",
  computed: {
    imgList() {
      return this.$page.frontmatter.carousels || this.$site.themeConfig.carousels || [];
    },
    logoImg(){
      return this.$site.themeConfig.logo
    }
  },
};
</script>
<style lang="stylus">
.header {
  position: relative;
  margin-bottom 20px;
  .app-title {
    position: absolute;
    top: 0;
    height: 60px;
    background-color: rgba(255, 255, 255, 0.3);
    width: 100%;
    margin: 0;
    z-index: 999;
    text-align: center;
  
    .app-logo {
      height: 50px;
      margin-top: 5px;
    }
  }
}

.carousel-img {
  width: 100%;
  height: 100%;
}
</style>
