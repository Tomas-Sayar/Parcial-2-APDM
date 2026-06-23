<script setup>
defineProps({
  movie: {
    type: Object,
    required: true,
  },
  imageUrl: {
    type: Function,
    required: true,
  },
  formatYear: {
    type: Function,
    required: true,
  },
  genreLabel: {
    type: Function,
    required: true,
  },
})

defineEmits(['select'])
</script>

<template>
  <article class="movie-card card border-0 shadow-sm" @click="$emit('select', movie)">
    <img
      v-if="movie.poster_path"
      :src="imageUrl(movie.poster_path)"
      :alt="movie.title"
      class="card-img-top movie-poster"
    />
    <div v-else class="poster-placeholder d-flex align-items-center justify-content-center">
      Sin póster
    </div>
    <div class="card-body">
      <div class="d-flex justify-content-between gap-2">
        <h3 class="h6 card-title mb-1">{{ movie.title }}</h3>
        <span class="badge text-bg-dark">{{ formatYear(movie.release_date) }}</span>
      </div>
      <p class="text-secondary small mb-2">{{ genreLabel(movie.genre_ids) }}</p>
      <p class="card-text small text-truncate-3">{{ movie.overview || 'Sin descripción' }}</p>
      <div class="d-flex justify-content-between align-items-center">
        <span class="small text-warning fw-semibold">⭐ {{ movie.vote_average?.toFixed(1) || 'NO' }}</span>
      </div>
    </div>
  </article>
</template>
