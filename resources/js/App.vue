<template>
  <v-container>
    <v-layout row justify-center>
      <v-flex sm8 class="text-xs-left">
        <h1 style="font-weight:540">Which Facebook Accounts do you want add?</h1>
        <h2
          style="font-weight:540"
          class="mt-3"
        >Choose the facebook pages, groups and profiles that you would like add to your marketing-suite account</h2>
      </v-flex>
    </v-layout>

    <v-layout row justify-center>
      <v-flex sm8 mt-4>
        <v-text-field v-model="search" solo label="Enter Social Network name or keyword" clearable></v-text-field>
      </v-flex>
    </v-layout>

    <v-layout row justify-center>
      <v-flex sm8 mt-4>
        <h2 style="font-weight:540" class="mb-2">Pages</h2>
        <span
          style="font-weight:540; font-size:18px;"
        >You need to be a page admin or editor for any pagesyou want to add to marketint-suite</span>
      </v-flex>
    </v-layout>

    <!-- this is pages rendering -->
    <v-layout row justify-center>
      <v-flex sm8 mt-4>
        <v-flex sm8 v-for="(item,index) in info.meta.accounts.data" :key="index">
          <v-list>
            <v-list-tile>
              <v-list-tile-avatar>
                <img :src="item.picture.data.url" alt>
              </v-list-tile-avatar>
              <v-list-tile-content>
                <v-list-tile-title>{{ item.name }}</v-list-tile-title>
              </v-list-tile-content>
              <v-list-tile-action>
                <v-btn outline class="secondary" small>Add</v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-list>
        </v-flex>
      </v-flex>
    </v-layout>

    <v-layout row justify-center>
      <v-flex sm8 mt-4>
        <div style="border:1px solid #ccc" class="mt-3"></div>
      </v-flex>
    </v-layout>

    <!-- Personal profile section -->
    <v-layout row justify-center>
      <v-flex sm8 mt-4>
        <h2 style="font-weight:540" class="mb-2">Personal Profile</h2>
      </v-flex>
    </v-layout>

    <v-layout row justify-center>
      <v-flex sm8 mt-2 d-flex>
        <v-flex sm8>
          <v-list>
            <v-list-tile>
              <v-list-tile-avatar>
                <img :src="info.meta.picture.data.url" alt>
              </v-list-tile-avatar>
              <v-list-tile-content>
                <v-list-tile-title>{{ info.meta.name }}</v-list-tile-title>
              </v-list-tile-content>
              <v-list-tile-action>
                <v-btn outline class="secondary" small>Add</v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-list>
        </v-flex>
      </v-flex>
    </v-layout>

    <v-layout row justify-center>
      <v-flex sm8 mt-4 class="text-xs-center">
        <v-btn outline class="secondary">Done</v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
//import HelloWorld from './components/HelloWorld'

export default {
  name: "App",
  components: {
    //HelloWorld
  },
  data() {
    return {
      info: null,
      search: "",
      pages: []
    };
  },
  mounted() {
    axios.get("/token.json").then(response => {
      this.info = response.data;
      console.log(this.info);
    });

    // this.pages = this.info.meta.accounts.data;
  },
  watch: {
    // search: function(q) {
    //   console.log(q);
    //   if (q == null || q == "undefined" || q == "" || q.length == 0) {
    //     this.pages = this.info.meta.accounts.data;
    //     return;
    //   }
    //   this.pages = this.pages.filter(function(page) {
    //     return new RegExp(q.trim(), "i").test(page.name);
    //   }, q);
    // }
  },
  computed: {
    filteredList() {
      console.log(this.info.meta.accounts.data + " hello");
      return this.info.meta.accounts.data.filter(item => {
        return item.name.toLowerCase().includes(this.search.toLowerCase());
      });
    }
  },
  created() {}
};
</script>