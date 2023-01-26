<template>
  <div class="home">
    <div  v-if="!isError">
        <div class="box" v-if="!isUsersLoading">
          <Users :node="users"/>
        </div>
        <div class='preload' v-else>
          <img src="@/assets/gifs/loader.gif" alt="gif">
        </div>
    </div>
    <div class="error" v-else>
      <error-home/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Users from '@/components/Users.vue';
import ErrorHome from '@/components/ErrorHome.vue';
export default {
  name: 'HomeView',
  components: {
    Users, ErrorHome
  },
  data () {
    return {
      users: [],
      clicked: false,
      isUsersLoading: false,
      isError: false,
    }
  },
  methods: {
    async fetchUsers () {
      try {
        this.isUsersLoading = true;
        const response = await axios.get('https://json.medrocket.ru/users/');
        setTimeout( async () => {
          this.users = response.data
          this.isUsersLoading = false;
        }, 1000)
      } catch (error) {
        this.isError = true
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
.box {
  margin-top: 16px;
  display: flex;
}
.preload{
  padding: 420px 348px
}
.error {
  margin: 25% 25%;
}
</style>
