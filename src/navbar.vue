<template>
<div class="nav-bar">
    <label for="show-menu" class="show-menu"> <i class="fa fa-bars"></i></label>
    <input type="checkbox" id="show-menu" role="button">
    <ul id="menu">
        <li><a href="#">Home</a></li>
        <li><a href="#">Books </a></li>
        <li><a href="#">Magazines</a></li>
        <li><a href="#">E-Books</a></li>
        <li><a href="#">Account</a></li>
    </ul>
    </div>
</template>
<script>
export default {
    name:"NavBar"
}
</script>



<style scoped>
.nav-bar {
    display: inline-block;
    width:100%;
    background-color: #2f3036
}
.nav-bar ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.nav-bar li {
  display: inline-block;
  float: left;
  margin-right: 1px;
}

.nav-bar li a {
  display: block;
  min-width: 140px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #fff;
  background: #2f3036;
  text-decoration: none;
}
.nav-bar li:hover a {
  background: #19c589;
}
.nav-bar li:hover ul a {
  background: #f3f3f3;
  color: #2f3036;
  height: 40px;
  line-height: 40px;
}
.nav-bar li:hover ul a:hover {
  background: #19c589;
  color: #fff;
}

.nav-bar ul li a:hover + .hidden,
.hidden:hover {
  display: block;
}
.show-menu {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    text-decoration: none;
    color: #fff;
    background: #2f3036;
    text-align: center;
    padding: 10px 0;
    display: none;
}
/*Hide checkbox*/
.nav-bar input[type=checkbox]{
    display: none;
}
/*Show menu when invisible checkbox is checked*/
.nav-bar input[type=checkbox]:checked ~ #menu{
    display: block;
}
@media screen and (max-width: 760px) {
  .nav-bar ul {
    position: static;
    display: none;
  }
  .nav-bar li {
    margin-bottom: 1px;
  }
  .nav-bar ul li,
  li a {
    width: 100%;
  }

  /*Display 'show menu' link*/
    .show-menu {
        display:block;
    }
}
</style>


