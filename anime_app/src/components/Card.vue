<template>
	<div class="card">
		<a :href="anime.url" target="_blank">
			<img 
				:src="anime.image_url" 
				:alt="anime.title + ' Poster'" 
			/>
			<h3>{{ anime.title }}</h3>
		</a>
	</div>
</template>

<script>
export default {
	props: ['anime']
}
</script>
