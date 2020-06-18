<template>
  <div class="theme-container article">
    <el-card class="box-card">
      <div slot="header" class="clearfix article-title">
        <span>{{title}}</span>
        <div class="article-time" v-if="time">{{time}}</div>
      </div>
      <div class="article-content">
        <div class="article-text">
          <Content />
        </div>
      </div>
    </el-card>
  </div>
</template>
<script>
export default {
  name: "essay",
  computed: {
    title() {
      return this.$page.frontmatter.title || "";
    },
    time() {
      return this.$page.frontmatter.time || "";
    }
  }
};
</script>
<style lang="stylus">
.article {
  .clearfix:before, .clearfix:after {
    display: table;
    content: '';
  }

  .el-card__header, .el-card__body {
    padding: 10px 20px;
  }

  .clearfix:after {
    clear: both;
  }

  .article-title {
    width: 100%;
    text-align: center;
    font-size: 24px;
    font-weight: 600;
  }

  .article-time {
    text-align: center;
    color: #ccc;
    font-size: 14px;
    line-height: 20px;
    height: 20px;
  }

  .article-content {
    > .article-text {
      margin-top: 20px;
    }
  }
}
</style>