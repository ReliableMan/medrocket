<template>
  <div>
    <div class="level-1">
      <div class="level1-2" v-for="element in favorites" :key="element.id">
        <img @click.stop="notActiveStar(element.id)" class="star" src="@/assets/icons/Fav_added.svg" alt="star_active">
        <img class="photo150" @click="showModal(element.url)" :title=element.title :src=element.thumbnailUrl alt="150x150">
        <p class="description">{{ element.title }}</p>
      </div>
    </div>
      <dialog-window v-show="visible" @show="closeModal" :show="visible">
        <img :src=photo alt="600x600">
      </dialog-window>
  </div>
</template>

<script>
import DialogWindow from '@/components/DialogWindow.vue';
export default {
  name: 'Favorites',
  components: {
    DialogWindow
  },
  data () {
    return {
      favorites: [],
      visible: false,
      photo: []
    }
  },
  methods: {
    notActiveStar(photoId) {
      this.favorites = this.favorites.filter((el) => el.id !== photoId);
      localStorage.setItem('savedAlbums', JSON.stringify(this.favorites))
    },
    showModal(photo) {
      this.visible = true;
      this.photo = photo
    },
    closeModal() {
      this.visible = false;
    }
  }, 
  mounted () {
    const data = localStorage.getItem('savedAlbums');
    data ? this.favorites = JSON.parse(data) : '';
  }
}
</script>

<style scoped>
.level-1 {
  margin: 56px 105px 14px 105px; 
  max-width: 744px;
  display: flex;
  flex-wrap: wrap;
  gap: 42px
  }
.photo150 {
  display:flex; 
  border-radius: 5px;
  width: 150px;
  height: 150px;
}
.photo150:hover {
  cursor: pointer;
  box-shadow: 0 0 10px rgba(0,0,0,0.5)
}
.level1-2 {
  display: flex;
  flex-direction: column;
  position: relative;
}
.description {
  width: 150px; 
  text-align:left; 
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 150%;
  color: #787878;
}
.star {
  position: absolute;
  margin-left: 73%;
  margin-top: 5%;
}
.star:hover {
  cursor: progress;
}
</style>
