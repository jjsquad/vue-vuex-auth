<script>
  import sidebar from 'vue-strap/src/Aside.vue'
  import { links, LOGOUT_URL } from '../router/paths'

  export default {

    props: ['visible', 'user'],

    components: {
      sidebar
    },

    data () {
      return {
        showProfile: false,
        links
      }
    },

    computed: {
      profileAvatar () {
        return this.user.avatar_url || 'https://avatars2.githubusercontent.com/u/12722517?v=3&u=18bf882b10e7cde77ce61d35e03e9e01e4c0f151&s=140'
      },

      logoutPath () {
        return {
          path: LOGOUT_URL
        }
      }
    }
  }
</script>

<template>
  <div>
    <nav class="navbar navbar-default">
      <div class="navbar-header">
        <span class="navbar-brand">Vue/Vuex com JWT-Auth</span>
      </div>
      <template v-if="visible">
        <sidebar :show.sync="showProfile" placement="right" header="Perfil" :width="500">
          <div>
            <div class="row well-sm">
              <div class="col-md-3">
                <img :src="profileAvatar" width="64" height="64">
              </div>
              <div class="col-md-9">
                <span><strong>{{ user.name }}</strong></span>
              </div>
            </div>
          </div>
        </sidebar>
        <div class="collapse navbar-collapse">
          <ul class="nav navbar-nav navbar">
            <li v-for="link in links" :class="{ 'active': $route.path == link.path }">
              <template v-if="link.dropdown">
                <a href="#" @click="link.callback" class="navbar-link">
                  <template v-if="link.image">
                    <img :src="link.image.source" :class="link.image.class" :style="link.image.style">
                  </template>
                  <span>{{ user.name }}</span>
                </a>
              </template>
              <template v-else>
                <a href="#" v-link="{ path: link.path }" class="navbar-link">
                  <template v-if="link.image">
                    <img :src="link.image.source" :class="link.image.class" :style="link.image.style">
                  </template>
                  <template v-if="link.icon">
                    <i :class="link.icon"></i>
                  </template>
                  <span>{{ link.title }}</span>
                </a>
              </template>
            </li>
          </ul>
          <ul class="nav navbar-nav navbar-right">
            <li>
              <img :src="profileAvatar" class="img-circle" style="max-height:48px;width:auto;vertical-align:middle;">
            </li>
            <li>
              <a href="#" class="navbar-link" @click="showProfile = true">
                {{ user.name }}
              </a>
            </li>
            <li>
              <a href="#" v-link="logoutPath" class="navbar-link">
                <i class="glyphicon glyphicon-log-out"></i>
                <span>Sair</span>
              </a>
            </li>
          </ul>
        </div>
      </template>
    </nav>
  </div>
</template>