<template>
	<div id='movie-list'>
		<div v-if="filteredMovies.length">
			<movie-item v-for="movie in  filteredMovies"  
					:movie="movie.movie" 
					:sessions="movie.sessions" 
					:day="day">
			</movie-item>		
		</div>
		<div v-else-if="movies.length" class="no-results">
			No results.
		</div>
		<div v-else class="no-results">
			Loading..
		</div>
	</div>
</template>
<script>
import genres from '../util/genres.js';
import MovieItem from './MovieItem.vue';
	export default {
		props: ['genre', 'time', 'movies', 'day'],
		methods: {
			moviePassesGenreFilter(movie) {
				if (!this.genre.length) {
					return true;
				} else {
					let movieGenre = movie.movie.Genre.split(", ");
					let matched = true;
					this.genre.forEach(genre => {
						if (movieGenre.indexOf(genre) === -1) {
							matched = false;
						}
					});
					return matched;
				}
			}
		},
			sessionPassesTimeFilter() {
				return true;
			},
		computed: {
			filteredMovies() {
				return this.movies
					.filter(this.moviePassesGenreFilter);
			}
		},
		components: {
			MovieItem
		}

		

	}
</script>