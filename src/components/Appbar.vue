<template>
  <div>
    <v-app-bar
      color="deep-purple accent-4"
      dense
      dark
    >
      <v-app-bar-nav-icon
      @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Yomar</v-toolbar-title>

      <v-spacer></v-spacer>
    </v-app-bar>




    <!-- MODAL -->
    <v-navigation-drawer
      v-model="drawer"
      absolute
      temporary
    >
      <v-list-item>
        <v-list-item-avatar>
          <v-img src="https://www.w3schools.com/w3css/img_avatar2.png"></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>YOMAR QUISPE</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

    </v-navigation-drawer>
  </div>  
</template>

<script>
export default {
  data(){
    return{
      drawer:null
    } 
  }
}
</script>