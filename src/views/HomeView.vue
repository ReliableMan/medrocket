<template>
  <div class="home">
    <div class="container" >
      <Users :node="users"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Users from '@/components/Users.vue'
export default {
  name: 'HomeView',
  components: {
    Users
  },
  data () {
    return {
      users: [],
      clicked: false
    }
  },
  methods: {
    async fetchUsers () {
      try {
        const response = await axios.get('https://json.medrocket.ru/users/');
        this.users = response.data
      } catch (error) {
        console.error
      }
    }
  },
  mounted () {
    this.fetchUsers()
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 744px;
  display: flex;
  flex-direction: column;
}
.container {
  margin-top: 16px;
  display: flex;
}
.name{
  padding-left: 24px;
  font-style: normal;
  font-weight: 500;
  font-size: 22px;
  line-height: 130%;
  color: #1C1C1C;
}
</style>
