<template>   
  <v-app id="app">
    <v-navigation-drawer
      app
      v-model="drawer"  
      color="deep-purple"
      dark
      class="vnavdraw"      
    >
      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.link"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar 
      app
      color="deep-purple"
      dense
      dark
    >      
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title class="headline"><v-icon>mdi-virus</v-icon>MagicDas</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-menu left bottom>
        <template v-slot:activator="{ on }"> 
          <v-btn icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>Option {{n}}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
   
    <v-content>
        <v-container fluid>
          <transition name="fade">
            <router-view></router-view>
          </transition>
        </v-container>
    </v-content>

  </v-app>  
</template>

<script>

export default {
  name: 'App',

  components: {

  },

  data: () => ({
    drawer: false,

    items: [
      { title: 'Home', icon: 'mdi-view-dashboard', link:'/' },
      { title: 'About', icon: 'mdi-image', link:'/about' },
      { title: 'Portfolio', icon: 'mdi-help-box', link:'/portfolio' },
      { title: 'Contacts', icon: 'mdi-help-box', link:'/contacts' },
    ],
    right: null,
      
  }),
};
</script>

<style>
  .vnavdraw {
    padding-top: 64px;
  }
  .fade-enter-active, .fade-leave-active {
  transition-property: opacity;
  transition-duration: .25s;
}

.fade-enter-active {
  transition-delay: .25s;
}

.fade-enter, .fade-leave-active {
  opacity: 0;
}
</style>
