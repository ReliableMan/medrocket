<template>
  
  <div>
    

      <div v-for="(user, index) in node" :key="user.id">
        <div class="level-1">
          <img class="img" :class="{active: index === currentIndex - 1}" @click.stop="handlerUser(user.id)" src="@/assets/icons/Open.svg" alt="open-img" />
          <img class="img" :class="{active: index !== currentIndex - 1}" @click.stop="handlerUserClose" src="@/assets/icons/Close.svg" alt="close-img"/>
          <p class="name">{{user.name}}</p>
        </div>
        <div v-if="!isAlbumsLoading || index !== currentIndex - 1">
          <div v-for="(album, ind) in albums" :key="album.id">
            <div v-if="user.id === album.userId" class="level-2">
              <img :class="{active: ind === currentIndex2}" class="img" @click.stop="handlerAlbum(album.id, ind)"  src="@/assets/icons/Open.svg" alt="open-img" />
              <img :class="{active: ind !== currentIndex2}" class="img" @click.stop="handlerAlbumClose" src="@/assets/icons/Close.svg" alt="close-img"/>
              <p class="album" v-if="user.id === album.userId && albums.length">{{ album.title }}</p>
              </div>
                  <div v-if="!isPhotosLoading || index !== currentIndex - 1 || ind !== currentIndex2" class="level-3">
                  <div v-for="(photo, ind2) in photosAlbums" :key="photo.id" >
                    <div v-if="user.id === album.userId && album.id === photo.albumId">
                      <img :class="{active: tempData.some(el => el.title === photo.title ) }" @click.stop="handlerStar(ind2)" class="star" src="@/assets/icons/Fav_inactive.svg" alt="star_inactive">
                      <img :class="{active: !tempData.some(el => el.title === photo.title) }" @click.stop="notActiveStar(photo.id)" class="star" src="@/assets/icons/Fav_added.svg" alt="star_active">
                      <img class="photo150" @click="showModal(photo.url)" :title=photo.title :src=photo.thumbnailUrl alt="150x150">
                    </div>
                  </div>
                  </div>
                  <div class='preload' v-else><img src="@/assets/gifs/loader.gif" alt="gif"></div>
            </div>
          </div>
          <div class='preload' v-else><img src="@/assets/gifs/loader.gif" alt="gif"></div>
      </div>
      <dialog-window v-show="visible" @show="closeModal" :show="visible">
        <img :src=photo alt="600x600">
      </dialog-window>

   
  </div>
</template>

<script>
import axios from 'axios';
import DialogWindow from './DialogWindow.vue';
export default {
  name: 'Users',
  components: {
    DialogWindow
  },
  props: {
    node: Array,
  }, 
  data () {
    return {
      albums: [],
      photosAlbums: [],
      currentIndex: null,
      currentIndex2: null,
      tempData: [],
      visible: false,
      photo: [],
      isAlbumsLoading: false,
      isPhotosLoading: false,
    }
  },
  methods: {
    async handlerUser (id) {
      this.currentIndex = id;
      try {
        this.isAlbumsLoading = true
        setTimeout( async () => {
          const response = await axios.get(`https://json.medrocket.ru/albums?userId=${id}`);
          this.albums = response.data;
          this.isAlbumsLoading = false
        }, 1000)
      } catch (error) {
        console.error
      } finally {
      }
    },
    handlerUserClose () {
      this.currentIndex = null;
      this.albums = null;
    },
    async handlerAlbum (id, index) {
      this.currentIndex2 = index;
      try {
        this.isPhotosLoading = true;
        setTimeout( async () => {
          const response = await axios.get(`https://json.medrocket.ru/photos?albumId=${id}`);
          const result = response.data;
          this.photosAlbums = result.slice(0, 11);
          this.isPhotosLoading = false;
        }, 1000)
       } catch (error) {
        console.error
       }
    },
    handlerAlbumClose () {
      this.currentIndex2 = null;
      this.photosAlbums = null;
    },
    handlerStar(index) {
      this.tempData.push(this.photosAlbums[index]);
      localStorage.setItem('savedAlbums', JSON.stringify(this.tempData))
    },
    notActiveStar(photoId) {
      this.tempData = this.tempData.filter((el) => el.id !== photoId);
      localStorage.setItem('savedAlbums', JSON.stringify(this.tempData))
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
    data ? this.tempData = JSON.parse(data) : '';
    }
}
</script>

<style scoped>
.level-1 {
  display: flex; 
  padding-top: 12px
}
.img:hover {
  cursor: pointer
}
.name {
  padding-left: 24px;
  font-style: normal;
  font-weight: 500;
  font-size: 22px;
  line-height: 130%;
  color: #1C1C1C;
}
.level-2 {
  display: flex; 
  padding-left:56px; 
  flex-wrap: wrap
}
.level-3 {
  display:flex; 
  flex-wrap: wrap; 
  padding-left: 102px; 
  gap: 42px;
  position: relative;
}
.active {
  display: none
}
.album {
  padding-left: 24px;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 130%;
  color: #1C1C1C;
  transform: rotate(-0.05deg);
}
.star {
  position: absolute;
  margin-left: 5%;
  margin-top: 1%;
}

.star:hover {
  cursor: progress;
}

.photo150 {
  display:flex; 
  border-radius: 5px;
}
.photo150:hover {
  cursor: pointer;
  box-shadow: 0 0 10px rgba(0,0,0,0.5)
}
.preload{
  padding: 136px 348px
}
</style>
