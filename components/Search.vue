<template>

	<div class="search">
		<input type="text" v-model="keyword" >
	</div>
</template>

<script>
export default {

  name: 'Search',

  data () {
    return {
    	keyword: '',
    }
  },
  watch: {
  	keyword(){
  		this.$emit('handleKeyword',this.keyword);
  	}
  }
};
</script>

<style lang="css" scoped>
.search{
	text-align: center;
	padding: 30px;
}
.search input{
	padding: 20px;
	font-size: 50px;
}
</style>