<template>
  <div class="video-player">
    <div class="video-details">
      <div class="video-container">
        <iframe width="640" height="360" :src="currentVideo.url" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
      </div>
      <div>
        <h3>{{currentVideo.title}}</h3>
        <p>{{currentVideo.views}} views</p>
        <hr />
        <p>{{currentVideo.creator}}</p>
        <p>{{currentVideo.description}}</p>
      </div>
    </div>
    <div class="video-list">
      <div v-for="video in videos" :key="video.id" @click="selectVideo(video)">
        <div v-if="video.id != currentVideo.id" class="thumbnail">
          <div class="thumbnail-image">
            <img :src="video.image_thumbnail" />
          </div>
          <div class="thumbnail-info">
            <h3>{{video.title}}</h3>
            <p>{{video.creator}}</p>
            <p class="thumbnail-views">{{video.views}} Views</p>
          </div>
        </div>  
      </div>
    </div>
  </div>
</template>

<script>
import MoviesData from '../assets/movies_data.json'
export default {
  name: 'VideoPlayer',
  data () {
    return {
      videos: MoviesData,
      currentVideo: MoviesData[0]
    }
  },
  methods: {
    selectVideo (video) {
      this.currentVideo = video
      video.views += 1
    }
  }
}
</script>

<style scoped>
.video-player{
  display:flex;
  width:1200px;
  margin:auto;
}
.video-details {
  margin-right:40px;
  text-align: left;
}
.video-container{
  width: 100%;
  position: relative;
  padding-bottom: 56.25%;
  padding-top: 25px;
  height: 0;
}
.video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
.thumbnail {
  display: flex;
}
.thumbnail img {
  width: 168px;
}
.thumbnail-info{
  margin-left:20px;
  text-align: left;
}
.thumbnail h3 {
  font-size: 1rem;
  line-height: 1.6rem;
  color: #140e0d;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}
.thumbnail-views{
  font-size:14px;
  color: #606060;
}
</style>
