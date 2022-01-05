<template>
<div>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <form class="form-inline my-2">
      <input class="form-control-lg ml-2 mr-sm-2" v-model="tag" type="search" placeholder="Search" aria-label="Search">
      <button class="form-control-lg btn btn-outline-success my-2 my-sm-0" @click="search" type="submit">Search</button>
    </form>

    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-md-auto gap-2">
        <li class="nav-item rounded">
          <a class="nav-link active" aria-current="page" href="#"><i class="bi bi-house-fill me-2"></i>Home</a>
        </li>
        <li class="nav-item rounded">
          <a class="nav-link" href="#"><i class="bi bi-people-fill me-2"></i>About</a>
        </li>
        <li class="nav-item rounded">
          <a class="nav-link" href="#"><i class="bi bi-telephone-fill me-2"></i>Contact</a>
        </li>

      </ul>
    </div>
  </div>
</nav>
</div>

</template>


<script>
export default {
  data() {
    return {
      tag: "",
    }
  }
}
</script>



<style scoped>

</style>