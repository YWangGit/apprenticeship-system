<!-- themePath/layouts/GlobalLayout.vue -->
<template>
  <div id="global-layout">
    <navbar></navbar>
    <component :is="layout" />
    <Footnote></Footnote>
  </div>
</template>

<script>
import Navbar from "@theme/components/Navbar.vue";
import Footnote from "@theme/components/Footnote.vue";
export default {
  components: {
    Navbar,
    Footnote
  },
  computed: {
    layout() {
      if (this.$page.path) {
        if (this.$frontmatter.layout) {
          // 你也可以像默认的 globalLayout 一样首先检测 layout 是否存在
          return this.$frontmatter.layout;
        }
        return "Layout";
      }
      return "NotFound";
    }
  }
};
</script>