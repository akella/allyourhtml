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
      let keyword = this.searchString.toLowerCase();

      let results = this.streams.filter(stream=>{
        if(stream.title.toLowerCase().indexOf(keyword)!==-1) return stream;
        if(stream.tags.filter(tag=>tag.toLowerCase().indexOf(keyword)!==-1).length>0) return stream;
        return false;
      })

      return results;
    }
  },
  methods: {
    setKeyword(keyword) {
      this.searchString = keyword;
    }
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
