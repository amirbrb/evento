<template>
  <div class="navigation-bar">
    <div class="header div12">
      <div class="menu-item" ref="menuSettings" v-show="this.$store.state.userData.authenticated">
        <router-link to="/settings">
          <font-awesome-icon icon="cog" class="button-small clickable"/>
        </router-link>          
      </div>
      <div class="menu-item" ref="menuList" v-show="this.$store.state.userData.authenticated">
        <router-link to="/list">
          <font-awesome-icon icon="list-ul" class="button-small clickable"/>
        </router-link>          
      </div>
      <div class="menu-item" ref="menuGeo" v-show="this.$store.state.userData.authenticated">
        <router-link to="/geo">
          <font-awesome-icon icon="globe" class="button-small clickable"/>
        </router-link>          
      </div>
      <router-link to="/">
        <div class="logo right">
          JABULEL<em style="font-style: italic; font-weight: 100;">A</em>
        </div>
      </router-link>
      <router-link to="/me" v-show="this.$store.state.userData.authenticated">
        <div class="user-settings right"> 
          <img class="user-profile button-small clickable" :src="getImage(this.$store.state.userData.profileImage)"/>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
  import imageService from '../../mixins/imageService'
  export default {
    mixins: [imageService],
    components: {},
    data: function () {
      return {
      }
    },
    mounted: function () {
      this.setSelectedItemByRouteName(this.$route.name)
      console.log(this.$store.state.userData)
    },
    watch: {
      $route (to, from) {
        let menus = document.getElementsByClassName('menu-item')
        Array.from(menus).forEach(function (item) {
          item.classList.remove('selected')
        })
        this.setSelectedItemByRouteName(this.$route.name)
      }
    },
    methods: {
      setSelectedItemByRouteName: function (route) {
        if (route === 'geo') {
          this.$refs.menuGeo.classList.add('selected')
        }
        if (route === 'list') {
          this.$refs.menuList.classList.add('selected')
        }
        if (route === 'settings') {
          this.$refs.menuSettings.classList.add('selected')
        }
      }
    }
  }
</script>

<style scoped>
  .navigation-bar{
    background: #F8F8F8;
    padding-top: 10px;
    padding-left: 2px;
    height: 46px;
    z-index: 2;
    border-bottom: 2px solid #A0A0A0;
  }

  .logo{
    margin-left: 15px;
    font-size: 32px;
    font-weight: bold;
    color: #B22222;
    font-family: 'Indie Flower', cursive;
  }

  .user-profile {
    border-radius: 50px;
    border: 2px solid #A0A0A0;
    position: absolute;
    right: 10px;
  }

  .menu {
    margin-top: 13px;
    width: 100%;
    background: grey;
    text-align: center;
  }

  .menu-item{
    font-size: 20px;
    color: #383838;
    width: 40px;
    float: left;
    border-left: 1px solid #A0A0A0;
    text-align: center;
  }

  .menu-item.selected{
    background: #A8A8A8;
    color: white;
  }


  .menu-item:nth-of-type(1){
    border-left: 0;
  }
</style>