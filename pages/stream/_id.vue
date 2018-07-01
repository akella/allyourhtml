<template>
	<div>
		<h1>{{title}}</h1>
		<h2>{{description}}</h2>

		<p><nuxt-link to="/">GO BACK TO STREAMS</nuxt-link></p>
	</div>
</template>


<script>
import MYDATA from '../../data/index.json';

function getStreamById(id, streams){
	const result = streams.filter(stream=>stream.id===id);
	return result[0];
}

	export default {
		async asyncData({params}){
			let myid = parseInt(params.id);
			return getStreamById(myid,MYDATA);
		}
	};
</script>


<style>
	
</style>