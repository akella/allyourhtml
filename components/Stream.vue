<template>
	<!-- begin stream -->
	<div class="stream">
		<nuxt-link :to="'/stream/'+stream.id">
			<h2>{{stream.title}}</h2>
			<img :src="'/streamposters/'+stream.img" alt="">
		</nuxt-link>
	</div>
	<!-- end stream -->
</template>

<script>
	export default {
		props: {
			streamdata: {
				type: Object
			},
		},
		data(){
			return {
				stream: this.streamdata
			}
		}
	};
</script>

<style>
	.stream img{
		display: block;
		width: 100%;
	}
</style>