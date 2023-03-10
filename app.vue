<template>
  <div class="hello">
    <h1>Vue 3 example with video.js preroll</h1>
    <video id="content_video" class="video-js vjs-default-skin" controls preload="auto" width="640" height="360">
      <source src="http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4"
        type="video/mp4" />
    </video>
  </div>
</template>

<script>

import videojs from 'video.js';
import 'videojs-contrib-ads';
import 'videojs-ima';
// Styles
import 'video.js/dist/video-js.min.css';
import 'videojs-contrib-ads/dist/videojs-contrib-ads.css';
import 'videojs-ima/src/css/videojs.ima.css';

export default {
  name: 'VideoAd',
  data() {
    return {
      player: null,
    };
  },
  mounted() {

    this.player = videojs('content_video');
    this.player.ima({
      debug: true,
      id: 'content_video',
      adTagUrl: 'http://pubads.g.doubleclick.net/gampad/ads?slotname=/124319096/external/ad_rule_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dpremidpostpod%26deployment%3Dgmf-js&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=preroll&pod=1&ppos=1&lip=true&min_ad_duration=0&max_ad_duration=30000&vrid=6376&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0',
    });
    // this.player.ads(); use this not error
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bumper-ad>video {
  display: none;
}
</style>
