<template>
  <div class="container">
    <SearchBar @termChange="onTermChange" />
    <div class="row">
      <VideoDetails :video="selectedVideo" />
      <VideoList
        :videos="videos"
        @videoSelect="onVideoSelect"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetails from './components/VideoDetails.vue';

const { VUE_APP_API_KEY: key } = process.env;
const url = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: 'App',
  components: { SearchBar, VideoList, VideoDetails },
  data() { return { videos: [], selectedVideo: null }; },
  methods: {
    onTermChange(q) {
      axios.get(url, {
        params: {
          key, type: 'video', part: 'snippet', q,
        },
      }).then(({ data }) => {
        this.videos = data.items;
      });
    },
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
  },
};
</script>
