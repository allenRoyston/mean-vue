<template language="pug"><div><h1>{{title}}</h1><cnavbar></cnavbar><home v-if="hash == 'home' || hash == ''"></home><about v-if="hash == 'about'"></about><images v-if="hash == 'images'"></images><contact v-if="hash == 'contact'"></contact><!-- FROM RENDER--><div style="height: 0; opacity: 0; position: absolute; z-index: -100;"><div id="___serverdata">{{device}}</div><div id="___vuepages">{{pages}}</div></div></div></template><script>export default {
  data: function() {
    return {
      title: "Vue/Express/Semantic UI Bootstrap",
      hash: null,
      server_data: {},
      server_pages: {}
    }
  },
  created:function(){
    var t = this;
    $(function(){

      // FROM SERVER DATA
      t.server_data = JSON.parse($('#___serverdata').text())
      t.server_pages = JSON.parse($('#___vuepages').text())

      // ROUTING
      t.setupRouting();
      $(window).bind( 'hashchange', function(e) {
        t.setupRouting();
      });

      // EVENT FROM EVENT EMITTER
      ee.addListener('changeUrl', function(response){
       window.location.hash = response.url;
      });

    })
  },
  methods:{
    setupRouting:function(){
      var t = this;
      var hashfull = window.location.hash.substr(1),
          hash = hashfull.split("&")[0];
          t.updateFromUrl(hash);
          setTimeout(function(){
            ee.emitEvent('urlchanged', [t.getParametersFromHash(hashfull)])
          }, 100)
    },
    getParametersFromHash:function(hashstring){
      var _r = {hash: hashstring.split("&")[0], params: [], query: []}
      for (var i = 1; i < (hashstring.match(/&/g) || []).length + 1; i++){
        _r.params.push({name: hashstring.split("&")[i]})
      }
      for (var i = 1; i < (hashstring.match(/\?/g) || []).length + 1; i++){
        _r.query.push({name: hashstring.split("?")[i]})
      }
      return _r;
    },
    updateFromUrl: function(new_hash){
      this.hash = new_hash
    }
  }
}</script><style lang="css">/* PENDING VUE-EXPRESS UPDATE */</style>