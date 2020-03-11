<template>
  <div
    class="card mb-3"
    style="max-width: 540px;margin: auto;"
  >
    <div class="row no-gutters">
      <div class="col-md-4">
        <a href="#">
          <img
            class="card-img"
            :src="restaurant.image"
          >
        </a>
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">
            {{ restaurant.name }}
          </h5>
          <span class="badge badge-secondary">收藏數：{{ restaurant.FavoriteCount }}</span>
          <p class="card-text">
            {{ restaurant.description }}
          </p>
          <router-link
            class="btn btn-primary mr-2"
            :to="{ name: 'restaurant', params: { id: restaurant.id }}"
          >
            Show
          </router-link>

          <button
            v-if="restaurant.isFavorited"
            type="button"
            @click.stop.prevent="deleteFavorite"
            class="btn btn-danger mr-2"
          >
            移除最愛
          </button>
          <button
            v-else
            type="button"
            @click.stop.prevent="addFavorite"
            class="btn btn-primary"
          >
            加到最愛
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    topRestaurant: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      restaurant: this.topRestaurant
    }
  },
  methods: {
    deleteFavorite () {
      this.restaurant.isFavorited = false
    },
    addFavorite () {
      this.restaurant.isFavorited = true
    }
  }
}
</script>
