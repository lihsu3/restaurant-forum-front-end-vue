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
          <span class="badge badge-secondary">收藏數：{{ updatedTopRestaurant.FavoriteCount }}</span>
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
            v-if="updatedTopRestaurant.isFavorited"
            type="button"
            @click.stop.prevent="deleteFavorite(restaurant.id)"
            class="btn btn-danger mr-2"
          >
            移除最愛
          </button>
          <button
            v-else
            type="button"
            @click.stop.prevent="addFavorite(restaurant.id)"
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
import usersAPI from './../apis/users'
import { Toast } from './../utils/helpers'

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
  computed: {
    updatedTopRestaurant: function () { 
      return this.topRestaurant
    }
  },
  methods: {
    async deleteFavorite (restaurantId) {
      try {
        const { data, statusText } = await usersAPI.deleteFavorite({
          restaurantId
        })

        if ((data.status !== "success") || (statusText !== "OK")) {
          throw new Error(statusText)
        }

        this.$emit('after-delete-favorite', restaurantId)
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: '無法取消收藏restaurant，請稍後再試'
        })
      }
    },
    async addFavorite (restaurantId) {
      try {
        const { data, statusText } = await usersAPI.addFavorite({
          restaurantId
        })

        if ((data.status !== "success") || (statusText !== "OK")) {
          throw new Error(statusText)
        }

        this.$emit('after-add-favorite', restaurantId)
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: '無法收藏restaurant，請稍後再試'
        })
      }
    }
  }
}
</script>
