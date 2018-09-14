<template>
  <div id="app">
    <div class="title"><h1>The Book Store</h1></div>
    <nav-bar></nav-bar>
    <book-list :width="window.width"/>
  </div>
</template>

<script>
import BookList from "./Books/BookList.vue";
import NavBar from './navbar.vue';
import Vue from "vue";
// DECLARATION
Vue.filter("truncate", function(value, length) {
  if (!value) {
    return "";
  }
  return value.substring(0, length);
});

export default {
  name: "app",
  components: {
    BookList,
    NavBar
  },
  data: function() {
    return {
      window: {
        width: 0,
        height: 0
      }
    };
  },
  created() {
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    }
  }
};
</script>

<style>
.title {
  text-align: center;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
* {
  box-sizing: border-box;
}

.selected{
  border: 1px solid green !important;
  background-color: green;
  opacity: 1;
  
}

.container {
  margin: 0 auto;
  padding: 0 0 2em 0;
  display: block;
}
.row {
  width: 100%;
  margin: 0;
  padding: 0;
  min-height: 200px;
  height: 100%;
}
.col-leftcontainer {
  width: 75%;
  height: auto;
}
.col-rightcontainer {
  width: 25%;
  height: auto;
}
.row::after {
  content: "";
  clear: both;
  display: table;
}
[class*="col-"] {
  float: left;
  vertical-align: top;
}
.col-1 {
  width: 8.33%;
}
.col-2 {
  width: 16.66%;
}
.col-3 {
  width: 25%;
}
.col-4 {
  width: 25%;
}
img {
  width: 100%;
  height: 200px;
  padding: 10px;
}
.padding-left-10 {
  padding-left: 10px;
}
.box {
  padding: 5px;
}
.mobile-view {
  display: none;
}
@media screen and (max-width: 768px) {
  .mobile-view {
    display: inline-block;
  }
  .desktop-view {
    display: none !important;
  }
  .col-leftcontainer {
    width: 100% !important;
    float: left;
  }
  .col-rightcontainer {
    width: 100%;
    float: left;
  }
  /* .col-leftcontainer{
        position: absolute;
    top: 85%;
  } */
  .col-5 {
    width: 100% !important;
  }
}
@media screen and (min-width: 769px) and (max-width: 1348px) {
  .col-leftcontainer {
    width: 75%;
    height: auto;
  }
  .col-rightcontainer {
    width: 25%;
    height: auto;
  }
  .col-5 {
    width: 50%;
  }
}

.col-5 {
  width: 50%;
}
.col-6 {
  width: 50%;
}
.col-7 {
  width: 58.33%;
}
.col-8 {
  width: 75%;
}
.col-9 {
  width: 75%;
}
.col-10 {
  width: 83.33%;
}
.col-11 {
  width: 91.66%;
}
.col-12 {
  width: 100%;
}

li {
  margin: 0 0 !important;
}
.featured {
  text-align: center;
}
.featured .col-4 {
  width: 100%;
  text-align: center;
}

.featured .col-8 {
  width: 100%;
}

.featured img {
  width: 50% !important;
}

.tile {
  width: 100%;
  border: 1px solid #000;
  height: auto;
  display: inline-block;
}
</style>
