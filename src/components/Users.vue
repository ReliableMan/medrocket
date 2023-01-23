<template>
  <!-- !! TO DO logic -->
  <div>
    <div style="display: flex" v-for="(user, index) in node" :key="user.id">
      <img v-if="user.id === index + 1" @click.stop="handle(user.id)" src="@/assets/icons/Open.svg" alt="open-img" />
      <img v-else src="@/assets/icons/Close.svg" alt="close-img"/>
      <p class="name">{{user.name}}</p>
      
      <div>
        <div v-for="album in albums" :key="album.id">
          <p v-if="user.id === album.userId">{{ album.title }}</p>
        </div>
      </div>

    </div>
    <!-- <TreeBrowser/> -->
    
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Users',
  props: {
    node: Array,
  }, 
  data () {
    return {
      albums: [],
    }
  },
  methods: {
    async handle (id) {
      console.log(id)
      const response = await axios.get(`https://json.medrocket.ru/albums?userId=${id}`);
      this.albums = response.data;
      console.log(this.albums);
    }
  }
}
</script>

<style lang="scss">
.name {
  padding-left: 24px;
  font-style: normal;
  font-weight: 500;
  font-size: 22px;
  line-height: 130%;
  color: #1C1C1C;
}

</style>
