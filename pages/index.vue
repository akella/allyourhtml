<template>
  <section class="container">
      <h1 class="title">
        allyourhtml!!11111
      </h1>

      <Search @handleKeyword="setKeyword" />
  
        <transition-group name="stream" class="stream-grid">
          <div v-for="stream in searchResultsStreams" :key="stream.id" class="stream-item">
            <Stream :streamdata="stream" />
          </div>
        </transition-group>

  </section>
</template>

<script>
import MYDATA from '../data/index.json';
import Stream from '@/components/Stream';
import Search from '@/components/Search';
import { debounce } from 'underscore';

export default {
  components: {
    Stream,
    Search
  },
  data(){
    return {
      streams: MYDATA,
      searchString: ''
    }
  },
  computed: {
    searchResultsStreams(){
      const keyword = this.searchString.toLowerCase();
      if (!keyword) return this.streams;
      const splittedKeyword = keyword.split(" ").filter(word => word);

      let results = this.streams.filter(stream => {
        let text = [
          stream.tags.join(' '),
          stream.title.toLowerCase(),
          stream.description.toLowerCase()
        ].join(' ');

        const matches = splittedKeyword.filter(keyword => text.includes(keyword));
        if (matches.length === splittedKeyword.length) {
          return true;
        }
        
        return false;
      });

      return results;
    }
  },
  methods: {
    setKeyword: debounce(function setKeyword(keyword) {
      this.searchString = keyword;
    }, 400),
  }
};
</script>

<style>
.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.stream{
  padding: 20px;
  background: #ccc;
  min-height: 100px;
}
.stream-grid{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px
}


.stream-item {
  transition: all 0.3s;
}
.stream-enter, .stream-leave-to{
  opacity: 0;
  transform: translateY(30px);
}
.stream-leave-active {
  position: absolute;
}
</style>
