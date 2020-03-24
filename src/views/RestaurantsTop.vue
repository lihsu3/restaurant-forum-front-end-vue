<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">
      人氣餐廳
    </h1>
    <hr>
    <TopRestaurantCard 
      v-for="topRestaurant in topRestaurants"
      :key="topRestaurant.id"
      :top-restaurant="topRestaurant"
      @after-add-favorite="afterAddFavorite"
      @after-delete-favorite="afterDeleteFavorite"
    />
  </div>
</template>

<script>
import NavTabs from '../components/NavTabs'
import TopRestaurantCard from '../components/TopRestaurantCard'
import restaurantsAPI from './../apis/restaurants'
import { Toast } from './../utils/helpers'

export default {
  components: {
    NavTabs,
    TopRestaurantCard
  },
  data () {
    return {
      topRestaurants: []
    }
  },
  created () {
    this.fetchTopRestaurants()
  },
  methods: {
    async fetchTopRestaurants () {
      try {
        const { data, statusText } = await restaurantsAPI.getTopRestaurants()

        if (statusText !== 'OK') {
          throw new Error(statusText)
        }

        this.topRestaurants = data.restaurants
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: '無法top restaurants，請稍後再試'
        })
      }
    },
    afterAddFavorite (restaurantId) {
      this.topRestaurants = this.topRestaurants.map(restaurant => {
        if (restaurant.id !== restaurantId) {
          return restaurant
        }

        return {
          ...restaurant,
          FavoriteCount: restaurant.FavoriteCount + 1,
          isFavorited: true
        }
      }).sort((a, b) => b.FavoriteCount - a.FavoriteCount)
    },
    afterDeleteFavorite (restaurantId) {
      this.topRestaurants = this.topRestaurants.map(restaurant => {
        if (restaurant.id !== restaurantId) {
          return restaurant
        }

        return {
          ...restaurant,
          FavoriteCount: restaurant.FavoriteCount - 1,
          isFavorited: false
        }
      }).sort((a, b) => b.FavoriteCount - a.FavoriteCount)
    }
  }
}
</script>
