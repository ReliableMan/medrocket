<template>
  <div class="home">
    <div  v-if="!isError">
        <div class="box" v-if="!isUsersLoading">
          <Users :node="users"/>
        </div>
        <div class='preload' v-else>
          <img class="size-svg" src="@/assets/gifs/preloader.svg" alt="preloader">
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
  display: flex;
  justify-content: center;
  padding-top: 30%;
  padding-left: 20%;
}
.error {
  margin: 25% 25%;
}
.size-svg{
  width: 200px;
  height: 200px;
}
</style>
