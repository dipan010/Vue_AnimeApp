<template>
	<div class="app">
		<header>
			<h1>The<strong>Anime</strong>Database</h1>

			<form class="search-box" @submit.prevent="HandleSearch">
				<input 
					type="search" 
					class="search-field" 
					placeholder="Search for an anime..."
					required
					v-model="search_query" />
			</form>
		</header>
		<main>
			<div class="cards" v-if="animelist.length > 0">
				<Card 
					v-for="anime in animelist" 
					:key="anime.mal_id"
					:anime="anime" />
			</div>
			<div class="no-results" v-else>
				<h3>Sorry, we have no results...</h3>
			</div>
		</main>
	</div>
</template>

<script>
import { ref } from 'vue';
import Card from './components/Card';
export default {
	setup() {
		const search_query = ref("");
		const animelist = ref([]);
		const HandleSearch = async () => {
			animelist.value = await fetch(`https://api.jikan.moe/v3/search/anime?q=${search_query.value}`)
				.then(res => res.json())
				.then(data => data.results);
			search_query.value = "";
		}
		return {
			Card,
			search_query,
			animelist,
			HandleSearch
		}
	}
}
</script>