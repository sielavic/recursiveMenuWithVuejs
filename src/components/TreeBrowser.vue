<template>
  <div>

    <div
        @click="nodeClicked"
        :style="{'margin-left': `${depth * 20}px`}"
        class="node"
    >



      <span
          v-if="this.$children.filter(el => el.isCheckedChildren).length === this.$children.length"
          class="input type"
      >{{ this.$children.length ? '&#9745;' : '' }}
      </span>


      <span
          v-if="hasChildren"
          class="type"
      >{{ catalog ? '&#45;' : '&#43;' }}
            </span>
      <span v-else> </span>
      {{ node.name }}
    </div>


    <input type="checkbox"
           v-model="isCheckedChildren"
           class="check"
    >


    <TreeBrowser
        v-if="catalog"
        v-for="child in node.children"
        :key="child.name"
        :node="child"
        :depth="depth + 1"
        @changeChildren="newNodeChecked"
        :nodeChecked="isCheckedChildren"
    />
  </div>
</template>

<script>
export default {
  name: 'TreeBrowser',
  props: {
    node: Object,
    depth: {
      type: Number,
      default: 0,
    },
    nodeChecked: Boolean,

  },
  data() {
    return {
      isCheckedChildren: this.nodeChecked,
      catalog: '',
    }
  },

  watch: {
    isCheckedChildren(variable) {
      this.node.checked = variable
      this.$emit('changeChildren', variable)
    },
    nodeChecked(variable) {
      this.isCheckedChildren = variable
    }

  },

  methods: {
    nodeClicked() {
      this.catalog = !this.catalog
    },

    newNodeChecked() {
      if (this.$children.filter(el => el.isCheckedChildren).length === this.$children.length) {
        this.isCheckedChildren = true
      } else {
        // this.isCheckedChildren = false
      }


    },


  },

  mounted() {
    this.checked = this.isCheckedChildren = this.node.checked;
  },

  computed: {
    hasChildren() {
      return this.node.children && this.node.children.length;
    }
  }
}
</script>

<style scoped>
.node {
  text-align: left;
  font-size: 18px;
  cursor: pointer;
  position: absolute;
}


.type {
  margin-left: 10px;
}
</style>
