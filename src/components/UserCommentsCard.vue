<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ commentedRestaurants.numOfCommentedRestaurants }}</strong> 已評論餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="restaurant in commentedRestaurants.restaurants"
        :key="restaurant.id"
        :to="{ name: 'restaurant', params: { id: restaurant.id }}"
      >
        <img :src="restaurant.image" width="60" height="60" class="avatar">
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    commentedRestaurants: {
      type: Object,
      required: true
    }
  }
}
</script>
