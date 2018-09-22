<template>
  <div>
    <SearchBar @termChange="onTermChange" />
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';

const { VUE_APP_API_KEY: key } = process.env;
const url = 'https://www.googleapis.com/youtube/v3/search';

export default {
  name: 'App',
  components: { SearchBar },
  methods: {
    onTermChange(q) {
      axios.get(url, {
        params: {
          key, type: 'video', part: 'snippet', q,
        },
      }).then(({ data }) => {
        console.log(data);
      });
    },
  },
};
</script>
