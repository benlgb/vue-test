<template>
  <div id="app">
    <file-node v-for="n in nodes" :data="n" :key="n.id"></file-node>
  </div>
</template>

<script>
import axios from "axios";
import { urls } from "./settings";
import FileNode from "./FileNode";

export default {
  name: "App",
  components: {
    FileNode
  },
  data() {
    return {
      nodes: [
        {
          id: "0",
          title: "正在加载节点数据"
        }
      ]
    };
  },
  async created() {
    let res = await axios.get(urls.nodes);
    this.$set(this, "nodes", res.data.msg);
  }
};
</script>

<style>
</style>
