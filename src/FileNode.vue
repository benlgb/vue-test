<template>
  <keep-alive>
    <div class="file-node" :id="data.id">
      <img class="node-icon" 
        :class="{'node-tree': isTree,
          'show-next': isTree&&showNext}" 
        :src="icon.source" 
        :alt="icon.title" 
        @click="toggleChildren"/>
      <span class="node-title" 
        :class="{'node-tree': isTree}"
        v-text="data.title" 
        @click="toggleChildren"></span>
      <div class="next-node" v-if="isTree && showNext">
        <file-node v-for="n in data.next" :data="n" :key="n.id"></file-node>
      </div>
    </div>
  </keep-alive>
</template>

<script>
import { icons } from "./settings";

export default {
  name: "FileNode",
  props: ["data"],
  data() {
    return {
      showNext: true
    };
  },
  computed: {
    isTree() {
      return !!this.data.next;
    },
    icon() {
      if (this.isTree) {
        return {
          title: "tree",
          source: icons.tree
        };
      } else {
        return {
          title: "file",
          source: icons.file
        };
      }
    }
  },
  methods: {
    toggleChildren() {
      this.showNext = !this.showNext;
      console.log(this.showNext);
    }
  }
};
</script>

<style scoped>
.node-info {
  float: left;
  clear: both;
}

.node-tree {
  cursor: pointer;
}

.node-icon {
  position: relative;
  top: 1px;
  width: 1em;
}

.node-icon.show-next {
  transform: rotate(90deg);
}

.next-node {
  margin-left: 1.2em;
}
</style>