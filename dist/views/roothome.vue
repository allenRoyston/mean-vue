<template language="pug"><div><h1>{{title}}</h1><!--p Welcome to the Vue/Express demo!
ul
  li(v-for="i in links")
     <a v-bind:href='i.link'>{{ i.title }}</a>
home(v-if="hash == 'home' || hash == ''")
about(v-if="hash == 'about'")
images(v-if="hash == 'images'")
small
hr
small isMobile: {{device.isMobile}}--></div></template><script>export default {
  data: function() {
    return {
      title: "Vue Component",
      hash: null,
      links:[
        {title: "Home", link: "#home"},
        {title: "About", link: "#about"},
        {title: "Images", link: "#images"}
      ],
      users: [
        {name: "John", age: 32},
        {name: "Smith", age: 23}
      ],
    }
  },
  created:function(){
    var t = this;
    $(function(){
      var hash = window.location.hash.substr(1);
      t.updateFromUrl(hash);
      $(window).bind( 'hashchange', function(e) {
        var hash = window.location.hash.substr(1);
        t.updateFromUrl(hash);
      });
    })

  },
  methods:{
    updateFromUrl: function(new_hash){
      this.hash = new_hash
    }
  }
}</script><style lang="css">/* PENDING VUE-EXPRESS UPDATE */</style>