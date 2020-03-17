<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img 
          :src="userProfile.image" 
          width="300px" 
          height="300px"
        >
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ userProfile.name }}</h5>
          <p class="card-text">
            {{ userProfile.email }}
          </p>
          <ul class="list-unstyled list-inline">
            <li><strong>{{ numOfCommentedRestaurants }}</strong> 已評論餐廳</li>
            <li><strong>{{ numOfFavoritedRestaurants }}</strong> 收藏的餐廳</li>
            <li><strong>{{ numOfFollowings }}</strong> followings (追蹤者)</li>
            <li><strong>{{ numOfFollowers }}</strong> followers (追隨者)</li>
          </ul>
          <p></p>
          <button 
            v-if="currentUser.id === userProfile.id"
            type="button" 
            class="btn btn-primary"
          >
            Edit
          </button>
          <button 
            v-else-if="checkIsFollowed"
            type="button" 
            class="btn btn-danger"
            @click.stop.prevent="unfollow"
          >
            取消追蹤
          </button>
          <button 
            v-else
            type="button" 
            class="btn btn-primary"
            @click.stop.prevent="follow"
          >
            追蹤
          </button>
          <p></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const dummyUser = {
  currentUser: {
    id: 1,
    name: '管理者',
    email: 'root@example.com',
    image: 'https://i.pravatar.cc/300',
    isAdmin: true
  },
  isAuthenticated: true
}

export default {
  props: {
    userProfile: {
      type: Object,
      required: true
    },
    numOfCommentedRestaurants: {
      type: Number,
      required: true
    },
    numOfFavoritedRestaurants: {
      type: Number,
      required: true
    },
    numOfFollowings: {
      type: Number,
      required: true
    },
    numOfFollowers: {
      type: Number,
      required: true
    },
    isFollowed: {
      type: Boolean,
      required: true
    }
  },
  data () {
    return {
      checkIsFollowed: this.isFollowed,
      currentUser: dummyUser.currentUser
    }
  },
  methods: {
    unfollow () {
      this.checkIsFollowed = false
    },
    follow () {
      this.checkIsFollowed = true
    }
  }
}
</script>
