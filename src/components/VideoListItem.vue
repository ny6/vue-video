<template>
  <li
    class="media list-group-item"
    @click="onVideoSelect"
  >
    <img
      :src="thumbnailUrl"
      :alt="video.snippet.title"
      class="mr-3"
    >
    <div class="media-body">
      <h5 class="mt-0 mb-1">{{ video.snippet.title }}</h5>
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    video: {
      type: Object,
      required: true,
    },
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    },
  },
  methods: {
    onVideoSelect() {
      this.$emit('videoSelect', this.video);
    },
  },
};
</script>
