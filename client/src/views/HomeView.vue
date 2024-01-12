<script>
import Vue from "vue";
import NavBar from "./components/NavBar.vue";
import { defineAsyncComponent } from "vue";
export default Vue.extend({
  name: "HomeView",
  components: {
    NavBar,
    SideBar: defineAsyncComponent(() => import("./components/SideBar.vue")),
  },
});
</script>

<template>
  <div>
    <nav-bar />
    <b-row class="w-100">
      <b-col cols="12" sm="12" md="2">
        <side-bar />
      </b-col>
      <b-col cols="12" sm="12" md="10" class="mt-3">
        <div class="mb-3"><h3>Contenido principal</h3></div>
        <b-row>
          <b-col cols="12" sm="6" md="4" lg="3" v-for="index in 10" :key="index">
            <div>
              <b-card
                title="Card Title"
                img-src="https://picsum.photos/600/300/?image=25"
                img-alt="Image"
                img-top
                tag="article"
                style="max-width: 20rem"
                class="my-3"
              >
                <b-card-text>
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </b-card-text>
              </b-card>
            </div>
          </b-col>
        </b-row>
      </b-col>
    </b-row>
  </div>
</template>
