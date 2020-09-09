<template>
  <div class="theme-container">
    <el-card class="box-card">
      <div slot="header" class="clearfix file-title">
        <el-page-header @back="goBack" :content="title"></el-page-header>
      </div>
      <div class="file-content">
        <div class="file-iframe">
          <iframe :src="$withBase(url)" width="100%" height="100%" frameborder="1"></iframe>
        </div>
        <div class="file-tip">
          如果你无法在线阅读文档,请点击
          <el-button @click="download(url,title)" type="text">{{title||'文件'}}</el-button>下载文件查看！
        </div>
        <Content />
      </div>
    </el-card>
  </div>
</template>
<script>
export default {
  name: "File",
  data() {
    return {};
  },
  computed: {
    title() {
      return this.$page.frontmatter.title || "";
    },
    url() {
      return this.$page.frontmatter.url || "";
    },
  },
  methods: {
    /**
     * 获取 blob
     * @param  {String} url 目标文件地址
     * @return {cb}
     */
    getBlob(url, cb) {
      const xhr = new XMLHttpRequest();
      xhr.open("GET", url, true);
      xhr.responseType = "blob";
      xhr.onload = function () {
        if (xhr.status === 200) {
          cb(xhr.response);
        }
      };
      xhr.send();
    },

    /**
     * 保存
     * @param  {Blob} blob
     * @param  {String} filename 想要保存的文件名称
     */
    saveAs(blob, filename) {
      if (window.navigator.msSaveOrOpenBlob) {
        navigator.msSaveBlob(blob, filename);
      } else {
        const link = document.createElement("a");
        const body = document.querySelector("body");

        link.href = window.URL.createObjectURL(blob);
        link.download = filename;

        // fix Firefox
        link.style.display = "none";
        body.appendChild(link);

        link.click();
        body.removeChild(link);

        window.URL.revokeObjectURL(link.href);
      }
    },

    /**
     * 下载
     * @param  {String} url 目标文件地址
     * @param  {String} filename 想要保存的文件名称
     */
    download(url, filename) {
      let downlaodUrl = String(url).replace(
        /^http(s)?:/,
        window.location.protocol
      );
      const realFilename = filename || downlaodUrl.split("/").pop();
      this.getBlob(downlaodUrl, (blob) => {
        this.saveAs(blob, realFilename);
      });
    },
    goBack() {
      this.$router.go(-2);
    },
  },
};
</script>
<style lang="stylus">
.clearfix:before, .clearfix:after {
  display: table;
  content: '';
}

.clearfix:after {
  clear: both;
}

.file-title {
  width: 100%;
  text-align: center;
  font-size: 24px;
  font-weight: 600;
}

.file-content {
  > .file-iframe {
    height: 700px;
  }

  > .file-tip {
    margin-top: 20px;
  }
}
</style>