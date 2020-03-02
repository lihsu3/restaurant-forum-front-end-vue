<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">
      美食達人
    </h1>
    <hr>
    <div class="row text-center">
      <TopUserCard 
        v-for="topUser in topUsers"
        :key="topUser.id"
        :top-user="topUser"
      />
    </div>
  </div>
</template>

<script>
import NavTabs from '../components/NavTabs'
import TopUserCard from '../components/TopUserCard'

const dummyDate = {
    "users": [
        {
            "id": 1,
            "name": "root",
            "email": "root@example.com",
            "password": "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
            "isAdmin": true,
            "image": null,
            "createdAt": "2020-02-28T14:38:32.000Z",
            "updatedAt": "2020-02-28T14:38:32.000Z",
            "Followers": [
                {
                    "id": 1,
                    "name": "root",
                    "email": "root@example.com",
                    "password": "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
                    "isAdmin": true,
                    "image": null,
                    "createdAt": "2020-02-28T14:38:32.000Z",
                    "updatedAt": "2020-02-28T14:38:32.000Z",
                    "Followship": {
                        "followerId": 1,
                        "followingId": 1,
                        "createdAt": "2020-02-29T08:11:44.000Z",
                        "updatedAt": "2020-02-29T08:11:44.000Z"
                    }
                }
            ],
            "FollowerCount": 1,
            "isFollowed": true
        },
        {
            "id": 2,
            "name": "user1",
            "email": "user1@example.com",
            "password": "$2a$10$NyaAtgRuHx3i7hHlnb5IXOC4Uk4.q1J1iQs3op.ymdCEh7.tOwcH2",
            "isAdmin": false,
            "image": null,
            "createdAt": "2020-02-28T14:38:32.000Z",
            "updatedAt": "2020-02-28T14:38:32.000Z",
            "Followers": [
                {
                    "id": 1,
                    "name": "root",
                    "email": "root@example.com",
                    "password": "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
                    "isAdmin": true,
                    "image": null,
                    "createdAt": "2020-02-28T14:38:32.000Z",
                    "updatedAt": "2020-02-28T14:38:32.000Z",
                    "Followship": {
                        "followerId": 1,
                        "followingId": 2,
                        "createdAt": "2020-03-01T16:26:37.000Z",
                        "updatedAt": "2020-03-01T16:26:37.000Z"
                    }
                }
            ],
            "FollowerCount": 1,
            "isFollowed": true
        },
        {
            "id": 3,
            "name": "user2",
            "email": "user2@example.com",
            "password": "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
            "isAdmin": false,
            "image": null,
            "createdAt": "2020-02-28T14:38:32.000Z",
            "updatedAt": "2020-02-28T14:38:32.000Z",
            "Followers": [],
            "FollowerCount": 0,
            "isFollowed": false
        },
        {
            "id": 62,
            "name": "AC",
            "email": "ac@ac.com",
            "password": "$2a$10$yB01LxQAujWjRQ0WaprYV.t5SDx6kool5Cmrt0F7TRSXGRk.W8z1m",
            "isAdmin": false,
            "image": null,
            "createdAt": "2020-02-29T15:41:09.000Z",
            "updatedAt": "2020-02-29T15:41:09.000Z",
            "Followers": [],
            "FollowerCount": 0,
            "isFollowed": false
        },
        {
            "id": 72,
            "name": "mohammad akhbarati",
            "email": "makhbarati@gmail.com",
            "password": "$2a$10$ljaWKqtQwgLA5BdTEhBTHeJK/Ku4ow3IHM4S5OJYmr7.anBAIl7NW",
            "isAdmin": false,
            "image": null,
            "createdAt": "2020-02-29T23:24:32.000Z",
            "updatedAt": "2020-02-29T23:24:32.000Z",
            "Followers": [],
            "FollowerCount": 0,
            "isFollowed": false
        }
    ]
}

export default {
  components: {
    NavTabs,
    TopUserCard
  },
  data () {
    return {
      topUsers: []
    }
  },
  created () {
    this.fetchTopUsers()
  },
  methods: {
    fetchTopUsers () {
      this.topUsers = dummyDate.users
    }
  }
}
</script>
