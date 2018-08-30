<template>
  <div id="home" class="home" style="height: 500px; overflow: auto">
    <img alt="Vue logo" src="../assets/logo.png" style="height: 1200px">
    <HelloWorld v-if="show" msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import { debounce } from 'lodash'
// @ is an alias to /src
const HelloWorld = () => import(/* webpackChunkName: "hello_world" */ '@/components/HelloWorld.vue')

export default {
  name: "home",
  components: {
    HelloWorld
  },
  data() {
    return {
      show: false
    };
  },
  mounted() {
    function getScrollTop() {
      var scrollTop = 0;
      // if (document.documentElement && document.documentElement.scrollTop) {
      //   scrollTop = document.documentElement.scrollTop;
      // } else if (document.body) {
      //   scrollTop = document.body.scrollTop;
      // }
      scrollTop = document.getElementById('home').scrollTop
      return scrollTop;
    }
    function getClientHeight() {
      var clientHeight = 0;
      if (document.body.clientHeight && document.documentElement.clientHeight) {
        clientHeight = document.body.clientHeight < document.documentElement.clientHeight ? document.body.clientHeight : document.documentElement.clientHeight;
      } else {
        clientHeight = document.body.clientHeight > document.documentElement.clientHeight ? document.body.clientHeight : document.documentElement.clientHeight;
      }
      return clientHeight;
    }
    function getScrollHeight() {
      return Math.max(document.body.scrollHeight, document.documentElement.scrollHeight);
    }
    function scrollAtBottom() {
      if (getScrollTop() + getClientHeight() >= getScrollHeight()) {
        return true;
      } else {
        return false;
      }
    }
    let that = this;
    document.getElementById('home').addEventListener('scroll', debounce(function() {
      if (scrollAtBottom()) {
        that.show = true;
      }
    }, 500));
  },
  methods: {}
};
</script>
