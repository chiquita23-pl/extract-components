<script setup>

import { StarIcon, TrashIcon, PencilIcon } from "@heroicons/vue/24/solid";
import { computed } from "vue";

const props = defineProps({
  movie: {
    id: Number,
    name: String,
    genres: Array,
    description: String,
    image: String,
    rating: Number,
  },
  movieIndex: Number  
});

const emit = defineEmits(["updateRating", "editMovie", "removeMovie"]);
</script>

<template>
  <div class="movie-item group">
        <div class="movie-item-image-wrapper">
          <div class="movie-item-star-wrapper">
            <StarIcon
              id="rating"
              class="movie-item-star-rating-icon"
              :class="[props.movie.rating ? 'text-yellow-500' : 'text-gray-500']"
            />
            <div class="movie-item-star-content-wrapper">
              <span
                v-if="props.movie.rating"
                id="rating-stars"
                class="movie-item-star-content-rating-rated"
              >
                {{ props.movie.rating }}/5
              </span>
              <span v-else class="movie-item-star-content-rating-not-rated">
                -
              </span>
            </div>
          </div>
          <img :src="props.movie.image" class="movie-item-image" alt="" />
        </div>

        <div class="movie-item-content-wrapper">
          <div class="movie-item-title-wrapper">
            <h3 class="movie-item-title">{{ props.movie.name }}</h3>
            <div class="movie-item-genres-wrapper">
              <span
                v-for="genre in props.movie.genres"
                :key="`${props.movie.id}-${genre}`"
                class="movie-item-genre-tag"
                >{{ genre }}</span
              >
            </div>
          </div>
          <div class="movie-item-description-wrapper">
            <p class="movie-item-description">{{ props.movie.description }}</p>
          </div>
          <div class="movie-item-rating-wrapper">
            <span class="movie-item-rating-text">
              Rating: ({{ props.movie.rating }}/5)
            </span>
            <div class="movie-item-star-icon-wrapper">
              <button
                v-for="star in 5"
                :key="star"
                class="movie-item-star-icon-button"
                :class="[
                  star <= props.movie.rating ? 'text-yellow-500' : 'text-gray-500',
                ]"
                :disabled="star === props.movie.rating"
                @click="emit('updateRating', props.movie.id, star)"
              >
                <StarIcon class="movie-item-star-icon" />
              </button>
            </div>

            <div class="movie-item-actions-list-wrapper">
              <button
                class="movie-item-action-edit-button"
                @click="emit('editMovie', props.movie.id)"
              >
                <PencilIcon class="w-4 h-4" />
              </button>
              <button
                class="movie-item-action-remove-button"
                @click="emit('removeMovie', props.movie.id)"
              >
                <TrashIcon class="w-4 h-4" />
              </button>
            </div>
          </div>
        </div>
  </div>
</template>
