<template>
  <div class="video_player">
    <video id="video" class="video-js vjs-default-skin">
      <source
        src="http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4"
        type="video/mp4"
      />
    </video>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from "vue";
import videojs from "video.js";
import "videojs-contrib-ads";
import "videojs-ima";

// Styles
import "video.js/dist/video-js.min.css";
import "videojs-contrib-ads/dist/videojs-contrib-ads.css";
import "videojs-ima/src/css/videojs.ima.css";

//loading this script in head
useHead({
  script: [
    {
      src: "https://imasdk.googleapis.com/js/sdkloader/ima3.js",
    },
  ],
});

//videojs option
let videoOptions = {
  autoplay: "true",
  preload: "auto",
  fill: true, //填充模式
  fluid: true, //will wait for the video to load to calculate the aspect ratio of the video
  controls: true,
  responsive: true, //響應式內部按鈕
  playsinline: true,

  // Make the text track settings dialog not initialize.
  textTrackSettings: false,
  qualityLevels: true,
  controlBar: {
    fullscreenToggle: true, //全螢幕關閉
    pictureInPictureToggle: false, //子母畫面關閉
    liveDisplay: true, //live 字樣關閉
    volumePanel: {
      inline: true, //可以调整方向为水平(true)或者垂直(false)
    },
  },
  userActions: {
    doubleClick: false,
  },
  httpSourceSelector: {
    default: "high",
  },
};
//video
let player;

//Registers a callback to be called after the component has been mounted.
onMounted(() => {
  player = videojs("video", videoOptions, onReady);
});

//on video ready call this
function onReady() {
  var adsOptions = {
    debug: true,
    id: "video",
    adTagUrl:
      "http://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/ad_rule_samples&ciu_szs=300x250&ad_rule=1&impl=s&gdfp_req=1&env=vp&output=xml_vmap1&unviewed_position_start=1&cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&cmsid=496&vid=short_onecue&correlator=",
  };
  player.ima(adsOptions);
}

//Registers a hook to be called right before a component instance is to be unmounted.
onBeforeUnmount(() => {
  if (player != null) {
    player.dispose();
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bumper-ad > video {
  display: none;
}
</style>
