<template>
  <div class="theme-container home">
    <el-row :gutter="20">
      <el-col v-for="(block,blockIndex) in content" :key="blockIndex" :span="block.span||24">
        <div :class="[block.layout||'box-layout']">
          <div
            class="box-layout-header"
            :style="{'border-bottom':block.border?'1px solid #eaecef':'none'}"
            v-if="block.title"
          >
            <div class="box-layout-header-left">
              <img v-if="block.img" :src="block.img" />
              <span>{{block.title}}</span>
            </div>
            <div class="box-layout-header-right">
              <el-button type="text">{{block.btn}}</el-button>
            </div>
          </div>
          <el-row :gutter="20">
            <el-col v-for="(item,i) in block.list" :key="i" :span="item.span||24">
              <div class="box-layout-item-wrap" :style="{background:item.bg}">
                <div class="box-layout-item" @click="jump(item)">
                  <div class="box-layout-item-img" v-if="item.img">
                    <img :src="item.img" />
                  </div>
                  <div class="box-layout-item-title" v-if="item.title">
                    <p
                      v-if="Array.isArray(item.title)"
                      v-for="(titleItem,titleIndex) in item.title"
                      :key="titleIndex"
                    >
                      <span v-html="titleItem"></span>
                    </p>
                    <span v-else>{{item.title}}</span>
                  </div>
                  <div class="box-layout-item-time" v-if="item.time">{{item.time}}</div>
                  <div class="box-layout-item-text" v-if="item.text">{{item.text}}</div>
                </div>
              </div>
            </el-col>
          </el-row>
        </div>
      </el-col>
    </el-row>
    <!-- markdown -->
    <Content />
  </div>
</template>
<script>
export default {
  name: "Home",
  computed: {
    content() {
      return this.$page.frontmatter.content
        ? this.$page.frontmatter.content
        : [];
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
.home {
  // 公共头部样式
  .box-layout-header {
    display: flex;
    height: 40px;
    line-height: 40px;
    padding: 10px;

    .box-layout-header-left {
      font-size: 25px;
      flex: 1;
      font-weight: bold;

      img {
        width: 30px;
        height: 30px;
        vertical-align: sub;
        margin: 0px 5px 0 0;
      }
    }

    .box-layout-header-right {
      width: 90px;

      .el-button {
        font-size: 16px;
        padding: 0 20px;
      }
    }
  }

  // 默认样式
  .box-layout {
    background-color: #FFF;
    color: #303133;
    transition: 0.3s;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
    padding: 0 20px;

    .box-layout-item-wrap {
      margin: 10px 0;

      .box-layout-item {
        text-align: center;
        cursor: pointer;
        padding: 10px;

        .box-layout-item-img {
          height: 50px;
          width: 50px;
          margin: 0 auto;

          img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
          }
        }

        .box-layout-item-title {
          padding-top: 10px;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }

        .box-layout-item-time {
          display: none;
        }

        .box-layout-item-text {
          display: none;
        }
      }
    }
  }

  // 文章列表样式
  .articles {
    .box-layout-item-wrap {
      margin-bottom: 20px;
      cursor: pointer;
      box-shadow: 0 2px 12px 2px #f8f6fa;
      border: none;
      color: #303133;
      padding: 0px 0px 0 2px;
      border-radius: 5px;

      .box-layout-item {
        background: #fff;
        border-radius: 5px 0 0 5px;
        padding: 10px 20px;
        position: relative;

        .box-layout-item-img {
          position: absolute;
          max-width: 200px;
          height: 70px;
          right: 20px;
          top: 50px;
          overflow: hidden;
          border-radius: 10px;

          img {
            height: 100%;
          }
        }

        .box-layout-item-title {
          font-size: 20px;
          padding-right: 100px;
          color: #000;
          margin: 0;
          font-weight: normal;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }

        .box-layout-item-time {
          position: absolute;
          max-width: 200px;
          height: 25px;
          line-height: 25px;
          right: 20px;
          top: 10px;
          overflow: hidden;
          color: #a4a7ae;
        }

        .box-layout-item-text {
          cursor: pointer;
          margin: 0;
          margin-top: 10px;
          height: 70px;
          line-height: 24px;
          color: #a4a7ae;
          word-break: break-all;
          text-overflow: ellipsis;
          overflow: hidden;
          display: -webkit-box;
          -webkit-line-clamp: 3;
          -webkit-box-orient: vertical;
          padding-right: 100px;
        }
      }
    }
  }

  // 排行榜样式
  .rankings {
    background-color: #FFF;
    transition: 0.3s;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
    padding: 10px 20px;

    .box-layout-item-wrap {
      .box-layout-item {
        .box-layout-item-img {
          display: none;
        }

        .box-layout-item-title {
          color: #545050;
          font-size: 16px;
          margin: 5px 0;
          width: 100%;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;

          &::before {
            content: '';
            display: inline-block;
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: #9c9ba3;
            vertical-align: middle;
            margin-right: 10px;
          }
        }

        .box-layout-item-time {
          display: none;
        }

        .box-layout-item-text {
          display: none;
        }
      }
    }
  }
}
</style>