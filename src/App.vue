<template>

  <div id="app">

    <button
        v-if="catalog"
        @click="reloadPage"
    >Сбросить значения
    </button>

    <button
        v-if="showTree"
        @click="hide"
    >Скрыть JSON
    </button>
    <button
        v-if="!showTree"
        @click="show"
    >Показать
    </button>

    <TreeBrowser
        :node="catalog"
        class="check"
    />

    <div v-if="showTree">
      <pre> {{ catalog }}</pre>
    </div>

  </div>

</template>
<script>

import TreeBrowser from "./components/TreeBrowser.vue";
import catalog from "./catalog.json";

export default {
  name: 'app',
  data() {
    return {
      catalog,
      showTree: [],
    }
  },
  methods: {
    show: function () {
      this.showTree = true
    },
    hide: function () {
      this.showTree = false
    },
    reloadPage() {
      window.location.reload();
    },

  },

  components: {
    TreeBrowser,
  }
}
</script>

<style>
button {
  margin-bottom: 34px;
}

.check {
  padding: 100px;
}


#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  margin-left: 311px
}
</style>