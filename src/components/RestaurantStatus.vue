<template>
  <div>
    <h1>{{ restaurant.name }}</h1>
    <span >{{ restaurant.categoryName }}</span>
    <hr>
    <ul>
      <li>有{{ restaurant.numOfComments }}筆評論</li>
      <li>有?人收藏這間餐廳</li>
    </ul> 
  </div> 
</template>

<script>
export default {
  props: {
    restaurantStatus: {
      type: Object,
      require: true
    }
  },
  data () {
    return {
      restaurant: this.restaurantStatus
    }
  }
}
</script>
