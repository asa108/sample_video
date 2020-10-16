<template>
  <div>
    <h1>Vuejs Hlsjs</h1>

    <video
      ref="video"
      id="video"
      controls
      webkit-playsinline
      muted
      autoplay
    ></video>
    <button @click="PlayVide()">動画を再生する</button>
    <button @click="changeResolution(3)" class="btn1">1080pを再生</button>
    <button @click="changeResolution(0)" class="btn2">360pを再生</button>

    <!-- <img src="../public/logo.png" alt="image" class="img" /> -->
    <!-- <img src="./assets/Icon_3d.png" alt="" /> -->
  </div>
</template>

<script>
import Hls from "hls.js";

export default {
  data() {
    return {
      // hlsjsを機能させるための初期化処理を格納した変数
      hls: new Hls(),
    };
  },
  methods: {
    PlayVide() {
      const video = document.getElementById("video");
      if (Hls.isSupported()) {
        this.hls = new Hls();
        // hls.currentLevel = n;
        this.hls.loadSource(
          "https://storage.googleapis.com/mahou_make/Assets/MAHOUMAKE_HLS/MAHOUMAKE_EYESHAOW.m3u8"
        );
        this.hls.attachMedia(video);
        this.hls.on(Hls.Events.MANIFEST_PARSED, function (event, data) {
          console.log(data.levels);
          console.log(event);
          this.hls.currentLevel();
          // hls.autoLevelEnabled = false;
          // hls.currentLevel = 3;
          video.play();
        });
      }
    },
    changeResolution(n) {
      console.log(n);
      // var video = document.getElementById("video");
      //ボタンにある引数を取ってきてそれをhls.currentLevelに代入することで
      //解像度が変わる
      //引数は取れてきてるけど、hls.currentLevelに入れれてない
      // var hls = new Hls();
      this.hls.currentLevel = n;

      console.log(n); //引数の値表示、1 or
      setTimeout(() => {
        console.log(this.hls.currentLevel);
      }, 1000);
    },
  },
};
</script>

<style>
#video {
  height: 300px;
}

/* .btn1{
  width: 100px;
  height: 100px;
} */
</style>
