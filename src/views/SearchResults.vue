<template>
  <div class="wrapper">
    <h1>Results for: "{{ tag }}"</h1>

    <div class="container">
      <div class="row g-3 py-6 mb-5">
        <div
          class="col-xs-12 col-sm-4"
          v-for="image in cleanImages"
          :key="image.id"
          :image="image"
        >
          <div class="card">
            <div class="card-image-wrapper">
              <img
                :src="image.url_n"
                class="img-fluid card-img-top"
                :alt="image.description"
              />
            </div>
            <div class="card-body">
              <h5 class="card-title">
                {{ image.title }}
              </h5>
              <p class="card-text">By : {{ image.ownername }}</p>
              <p class="card-text">Views : {{ image.views }}</p>
              <a href="#" class="btn btn-primary">View Image</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Pagination />
  </div>
</template>

<script>
import flickr from "../flickr";
import Pagination from "../components/Pagination.vue"

export default {
  name: "home",
  components:{
    Pagination
  },
  props: {
    tag: String,
  },
  created() {
    this.search();
  },
  watch: {
    tag(value) {
      this.search();
      console.log(value);
    },
  },
  data() {
    return {
      loading: false,
      images: [],
    };
  },
  methods: {
    search() {
      if (!this.isTagEmpty) {
        this.loading = true;
        console.log("i got here");
        this.fetchImages();
      }
    },
    fetchImages() {
      return flickr("photos.search", {
        tags: this.tag,
        extras: "url_n, owner_name, description, date_taken, views",
        page: 10,
        per_page: 15,
      }).then((response) => {
        this.images = response.data.photos.photo;
      });
    },
  },
  computed: {
    cleanImages() {
      return this.images.filter((image) => image.url_n);
    },
    isTagEmpty() {
      return !this.tag || this.tag.length === 0;
    },
  },
};
</script>
