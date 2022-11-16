<template>
  <v-app theme.dark:true>
    <v-app-bar app clipped-left>
      <v-app-bar-nav-icon />
      <v-icon class="mx-4" large>mdi-video</v-icon>
      <v-tolbar-title class="align-center">
        <span class="title">Video Play</span>
      </v-tolbar-title>
      <v-spacer />
      <v-text-field class="mt-5" placeholder="Ara..." id="search" name="search" color="black" solo single-line right="true" />
      <v-spacer />
      <v-btn class="ml-0" icon>
        <v-icon>mdi-apps</v-icon>
      </v-btn>
      <v-btn class="ma-2" icon>
        <v-icon>mdi-bell</v-icon>
      </v-btn>
      <div>
        <v-menu v-model="menu" :close-on-content-click="false" :nudge-width="450" offset-x>
          <template v-slot:activator="{ on }">
            <v-avatar size="40">
              <img v-on="on" @click="menu = true" width="40"
                src="data:image/jpeg;base64,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"
                alt="Serhat VARLİ" />
            </v-avatar>
          </template>

          <v-card>
            <v-list>
              <v-list-item>
                <v-list-item-vatar v-align-items-center>
                </v-list-item-vatar>
                <v-list-item-context>
                  <v-list-item-title>Serhat VARLİ</v-list-item-title>
                  <v-list-item-subtitle>Front End Developer</v-list-item-subtitle>
                </v-list-item-context>
              </v-list-item>
            </v-list>

            <v-divider />

            <v-list>
              <v-list-item>
                <v-list-item-action>
                  <v-icon>mdi-cog</v-icon>
                </v-list-item-action>
                <v-list-item-title>Settings</v-list-item-title>
              </v-list-item>
            </v-list>

            <v-list>
              <v-list-item class="d-flex">
                <v-list-item-action>
                  <v-switch v-model="theme" color="purple" />
                </v-list-item-action>
                <v-list-item-title>Theme Dark</v-list-item-title>
              </v-list-item>
            </v-list>
            <v-cart-actions>
              <v-spacer />
              <v-btn color="primary" class="w-100 mb-3" text @click="menu = false">
                Exit
              </v-btn>
            </v-cart-actions>

          </v-card>
        </v-menu>
      </div>

    </v-app-bar>
    <v-container class="mt-16">
      <v-row  class="mt-2">
        <v-col sm="6" md="4" xl="3" v-for="(item, index) in 200" :key="index">
          <v-card>
            <v-img :src="`https://picsum.photos/500/300?image=${index + 1}`" :leyz-src="`https://picsum.photos/10/10?image=${index + 1}`" />
            <v-cart-subtitle class="pa-4 d-block">title {{ index + 1 }}</v-cart-subtitle>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: "app",

  data: () => ({
    menu: false,
    theme: false,

  }),
  watch: {
    theme: function (next) {
      console.log("ilk -- "  +  this.$vuetify.theme.themes.light)
      console.log("next -- "  +  next)
      this.$vuetify.theme.primary = '#ff00ff';
      console.log("son -- "  +  this.$vuetify.theme.themes.light)
      console.log("next -- "  +  next)
    }
  }
}
</script>
