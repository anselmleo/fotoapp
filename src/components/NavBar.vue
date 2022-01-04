<template>
<div>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <!-- <a class="navbar-brand" href="#">Search Photos</a> -->

    <form class="form-inline my-2">
      <input class="form-control-lg ml-2 mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="form-control-lg btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
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
        <!-- <li class="nav-item dropdown rounded">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false"><i class="bi bi-person-fill me-2"></i>Profile</a>
          <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" href="#">Account</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li>
              <hr class="dropdown-divider">
            </li>
            <li><a class="dropdown-item" href="#">Logout</a></li>
          </ul>
        </li> -->
      </ul>
    </div>
  </div>
</nav>
</div>

</template>

<style scoped>

</style>