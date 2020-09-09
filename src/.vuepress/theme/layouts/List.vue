<template>
  <div class="theme-container list">
    <div v-if="title" class="list-title">
      <img class="datum-img" v-if="icon" :src="icon" alt="图标" />
      {{title}}
    </div>
    <el-row :gutter="12">
      <el-col  v-for="(item, index) in list" :key="index" :span="item.span||12">
        <el-card
          class="box-card"
          @click.native="jump(item)"
          :body-style="{background: item.bg||'#ffffff'}"
        >
          <div class="box-card-wrap">
            <div class="item-header">
              <div class="item-title">{{ item.title }}</div>
              <div class="item-time">{{ item.time }}</div>
            </div>
            <p class="item-desc" v-if="item.text">{{ item.text }}</p>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <Content />
  </div>
</template>
<script>
export default {
  name: "list",
  computed: {
    title() {
      return this.$page.frontmatter.title || "";
    },
    icon() {
      return this.$page.frontmatter.icon || "";
    },
    list() {
      return this.$frontmatter.list ? this.$frontmatter.list : [];
    }
  },
  methods: {
    jump(item) {
      if (!item.url) {
        return false;
      }
      open(this.$withBase(item.url), item.name || "_self");
    }
  }
};
</script>
<style lang="stylus">
.list {
  .list-title {
    text-align: left;
    color: #000;
    font-size: 24px;
    padding: 10px 0;
    font-weight: bold;
  }

  .datum-img {
    height: 25px;
    width: 25px;
    vertical-align: middle;
    margin-right: 10px;
  }

  .box-card {
    margin-bottom: 20px;
    cursor: pointer;
    box-shadow: 0 2px 12px 2px rgba(248, 246, 250, 1);
    border: none;

    .el-card__body {
      padding: 0px 0px 0 2px;
    }

    .box-card-wrap {
      background: #fff;
      border-radius: 5px 0 0 5px;
      padding: 10px 20px;
    }

    .item-header {
      position: relative;
      height: 40px;
      line-height: 40px;
      color: #999;
      cursor: pointer;

      > .item-title {
        font-size: 20px;
        padding-right: 150px;
        color: #000;
        margin: 0;
        font-weight: normal;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 1;
        overflow: hidden;
      }

      > .item-time {
        position: absolute;
        max-width: 200px;
        height: 40px;
        right: 0;
        top: 0;
        overflow: hidden;
        color: #a4a7ae;
      }
    }

    .item-desc {
      cursor: pointer;
      margin: 0;
      margin-top: 10px;
      height: 48px;
      line-height: 24px;
      color: #a4a7ae;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
  }
}
</style>