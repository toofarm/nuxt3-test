<template>
    <div>
        <form>
            <label for="query">Search for movies</label>
            <input 
                id='query'
                v-model="state.query"
                type="text"
                placeholder="Gone With the Wind, etc."
                name='query'
                />
            <button
                :disabled="state.query === ''"
                @click="(e) => doSearch(e)"
            >
                Submit
            </button>
        </form>
        <div 
            v-if="state.loading"
            class="loader">
            We're doing a loading
        </div>
        <ul
            v-if="state.movies.length > 0 && !state.loading"
            >
            <li 
                v-for="(movie) in state.movies"
                :key="movie.id">
                <h3>
                    {{ movie.title }}
                </h3>
                <p>
                    {{ movie.description }}
                </p>
            </li>
        </ul>
        <div 
            v-if="state.noResults && !state.loading"
            class="no-results">
            No results for that search
        </div>
    </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import axios from 'axios'
import { API_KEY } from '../lib/constants'

const state = reactive({ 
	query: '',
	movies: [],
	loading: false,
	noResults: false
})

const doSearch = async (e: Event) => {
	e.preventDefault()
	state.noResults = false
	state.loading = true

	const res = 
            await axios.get(`https://imdb-api.com/en/API/SearchMovie/${API_KEY}/${state.query}`)

	state.loading = false
    
	if (res.data.results.length < 1) {
		state.noResults = true
	}

	state.movies = res.data.results

}
</script>

<style>
    form label,
    form button { 
        display:  block;
        margin: 0.5rem 0;
    }

    form input {
        padding: 0.25em 0.5em;
        min-width: 200px;
    }

    .loader {
        padding: 1em;
        margin: 1em;
    }

    .no-results {
        padding: 1rem 0;
    }
</style>