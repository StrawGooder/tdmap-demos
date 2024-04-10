<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div id = "mapDiv"></div>
  </div>

</template>

<!-- <script src="http://api.tianditu.gov.cn/api?v=4.0&tk=5552493db63e98f85ae582b3429040c0"/> -->
<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
  },

  created(){


  },

  methods:{

    initMap(){

        // lay = new T.TileLayer(imageURL, {minZoom: 1, maxZoom: 18});
        // var config = {layers: [lay]};
        // //初始化地图对象
        // map = new T.Map("mapDiv", config);
        // //设置显示地图的中心点和级别
        // map.centerAndZoom(new T.LngLat(116.40969, 39.89945), zoom);
        // //允许鼠标滚轮缩放地图
        // map.enableScrollWheelZoom();

        var access_token = "5552493db63e98f85ae582b3429040c0"

        // var access_token_enc = encodeURIComponent(access_token);

        // console.log(`debug-token `, access_token_enc)


        var z = 8
        var x = 210
        var y = 96

        var map;
        var zoom = 8;
        // var imageURL = "http://t0.tianditu.gov.cn/img_w/wmts?" +
        //     "SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=img&STYLE=default&TILEMATRIXSET=w&FORMAT=tiles" +
        //     `&TILEMATRIX=${z}&TILEROW=${y}&TILECOL=${x}&tk=${access_token}`;

        var imageURL = "http://t0.tianditu.gov.cn/img_w/wmts?" +
            "SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=img&STYLE=default&TILEMATRIXSET=w&FORMAT=tiles" +
            `&TILEMATRIX={z}&TILEROW={y}&TILECOL={x}&tk=${access_token}`;

        var lay = new window.T.TileLayer(imageURL, {minZoom: 1, maxZoom: 16});
        var config = {layers: [lay]};
        // //初始化地图对象
        // // map = new window.T.Map("mapDiv", config);

        this.map = new window.T.Map("mapDiv", config);
       
        //设置显示地图的中心点和级别
        this.map.centerAndZoom(new window.T.LngLat(116.40969, 39.89945), zoom);
        //允许鼠标滚轮缩放地图
        this.map.enableScrollWheelZoom();
    }

  },

  mounted(){

    var head_elem = document.getElementsByTagName("head")[0];

    var script_elem = document.createElement("script")
  
    var target_url = "http://api.tianditu.gov.cn/api?v=4.0&tk=5552493db63e98f85ae582b3429040c0"

    script_elem.setAttribute("src", target_url)

    // console.log(`debug-html `, head_elem)

    head_elem.appendChild(script_elem)


    setTimeout(()=>{this.initMap()}, 2000);

  }

};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

/*  width: 100%;
  height: 50%;*/
/*  width: 1024px;
  height: 768px;*/
}

body {
  width: 100%;
  height: 100%;
}

#mapDiv {
  width: 100%;
  height: 400px;
}
</style>
