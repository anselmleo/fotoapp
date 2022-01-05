<template>
  <div>
    <div class="container">
      <div class="row g-3 py-6 mb-5">
        <h2 class="centered py-4">Browse the Latest Uploads</h2>
        <div
          class="col-xs-12 col-sm-4"
          v-for="image in recentPhotos"
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
              <router-link :to="{name:'photoDetails', params:{id: image.id, secret:image.secret}}">
                 <a href="#" class="btn btn-primary"  >View Image</a>
              </router-link>

            </div>
          </div>
        </div>
      </div>
      <div class="d-flex justify-content-center">
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <li class="page-item">
              <a class="page-link" v-if="firstPaginatorNumber >= 1" @click="handlePrevClick(firstPaginatorNumber-1)" href="#" aria-label="Previous">
                <span aria-hidden="true">&laquo;</span>
              </a>
            </li>
            <li class="page-item"><a class="page-link" @click="fetchRecentPhotos(1)" href="#">{{firstPaginatorNumber}}</a></li>
            <li class="page-item"><a class="page-link" @click="fetchRecentPhotos(2)" href="#">{{secondPaginatorNumber}}</a></li>
            <li class="page-item"><a class="page-link" @click="fetchRecentPhotos(3)" href="#">{{thirdPaginatorNumber}}</a></li>
            <li class="page-item">
              <a class="page-link" @click="handleNextClick(thirdPaginatorNumber+1)" href="#" aria-label="Next">
                <span aria-hidden="true">&raquo;</span>
              </a>
            </li>
          </ul>
        </nav>
  </div>
      <!-- <Pagination /> -->
    </div>
  </div>
</template>

<script>
import flickr from "../flickr";
// import NavBar from "../components/NavBar"
// import Pagination from "../components/Pagination.vue"
export default {
  name: "recentPhotos",
  components:{
    //  NavBar,
    // Pagination
  },
  created() {
    this.fetchRecentPhotos();
  },
  data() {
    return {
      recentPhotos: [],
      firstPaginatorNumber: 1,
      secondPaginatorNumber: 2,
      thirdPaginatorNumber: 3
    };
  },

  props: {
    tag: String,
  },

  methods: {
    fetchRecentPhotos(pageNumber = 1) {
      console.log("i got here2, pageNumber", pageNumber)
      return flickr("photos.getRecent", {

        extras: "url_n, owner_name, description, date_taken, views",
        page: pageNumber,
        per_page: 9,
      })
        .then((response) => {
          this.recentPhotos = response.data.photos.photo;
        })
        .catch((error) => {
          console.log("Error occured: ", error);
        });
    },

    incrementPaginatorNumbers(pageNumber) {
      if(pageNumber - this.firstPaginatorNumber > 2) {
        this.firstPaginatorNumber++
      }

      if(pageNumber - this.secondPaginatorNumber > 1) {
        this.secondPaginatorNumber++
      }

      if(pageNumber - this.thirdPaginatorNumber > 0 ) {
        this.thirdPaginatorNumber++
      }
    },

    decreasePaginatorNumbers(pageNumber) {
      if(this.thirdPaginatorNumber - pageNumber > 2) {
        this.firstPaginatorNumber--
      }

      if(this.secondPaginatorNumber - pageNumber > 1) {
        this.secondPaginatorNumber--
      }

      if(this.thirdPaginatorNumber - pageNumber > 0 ) {
        this.thirdPaginatorNumber--
      }
    },

    handleNextClick(pageNumber) {
      this.incrementPaginatorNumbers(pageNumber);
      this.fetchRecentPhotos(pageNumber);
    },

    handlePrevClick(pageNumber) {
      this.decreasePaginatorNumbers(pageNumber);
      this.fetchRecentPhotos(pageNumber);
    },


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
        this.recentPhotos = response.data.photos.photo;
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

<style>
  .card-img-top {
    height: 320px !important;
  }

  .card {
    height: 520px;
  }

</style>