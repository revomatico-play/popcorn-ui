<template>
  <v-list three-line>
    <template v-for="(item, index) in items">
      <v-subheader
        v-if="item.header"
        :key="item.header"
        v-text="item.header"
      ></v-subheader>

      <v-divider
        v-else-if="item.divider"
        :key="index"
        :inset="item.inset"
      ></v-divider>
      <v-list-item v-else :key="item.itemTitle">
        <v-list-item-avatar size="80">
          <v-btn :href="item.itemUrl" target="_blank">
            <v-img :src="item.itemImage"></v-img>
          </v-btn>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-btn :href="item.itemUrl" target="_blank">
            <v-list-item-title>
              {{ item.itemTitle }}
              ({{ item.itemSource }})</v-list-item-title
            >
          </v-btn>
          <v-list-item-subtitle
            v-html="item.itemDescription"
          ></v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </template>
  </v-list>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    items: []
  }),
  mounted() {
    console.log("Here we call the server for movies!!!");
    // this.items = [
    //   { header: "Today" },
    //   {
    //     itemImage: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
    //     itemTitle: "Brunch this weekend?",
    //     itemDescription:
    //       "<span class='text--primary'>Ali Connors</span> &mdash; I'll be in your neighborhood doing errands this weekend. Do you want to hang out?"
    //   },
    //   { divider: true, inset: true },
    //   {
    //     itemImage: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
    //     itemTitle:
    //       'Summer BBQ <span class="grey--text text--lighten-1">4</span>',
    //     itemDescription:
    //       "<span class='text--primary'>to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this weekend."
    //   },
    //   { divider: true, inset: true },
    //   {
    //     itemImage: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
    //     itemTitle: "Oui oui",
    //     itemDescription:
    //       "<span class='text--primary'>Sandra Adams</span> &mdash; Do you have Paris recommendations? Have you ever been?"
    //   },
    //   { divider: true, inset: true },
    //   {
    //     itemImage: "https://cdn.vuetifyjs.com/images/lists/4.jpg",
    //     itemTitle: "Birthday gift",
    //     itemDescription:
    //       "<span class='text--primary'>Trevor Hansen</span> &mdash; Have any ideas about what we should get Heidi for her birthday?"
    //   },
    //   { divider: true, inset: true },
    //   {
    //     itemImage: "https://cdn.vuetifyjs.com/images/lists/5.jpg",
    //     itemTitle: "Recipe to try",
    //     itemDescription:
    //       "<span class='text--primary'>Britta Holt</span> &mdash; We should eat this: Grate, Squash, Corn, and tomatillo Tacos."
    //   }
    // ];

    axios
      .get("http://localhost:8000/movies", {
        headers: {
          "Access-Control-Allow-Origin": "http://localhost:8000"
        }
      })
      .then(response =>
        // JSON responses are automatically parsed.
        {
          // eslint-disable-next-line no-console
          console.log("loaded", response);
          this.items = response.data;
        }
      )
      .catch(function(error) {
        if (error.response) {
          console.log(error.response.headers);
        } else if (error.request) {
          console.log(error.request);
        } else {
          console.log(error.message);
        }
        console.log(error.config);
      });
  }
};
</script>
