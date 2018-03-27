<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <a class="navbar-brand" href="#">DAPP Sentinela</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
  
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <router-link class="nav-link" href="#" to="/">Home <span class="sr-only">(current)</span></router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" href="#" to="/hello">Vue</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" href="#" to="/dash">Dashboard</router-link>
        </li>
        <li class="nav-item">
          <a class="nav-link disabled" href="#">Disabled</a>
        </li>
      </ul>
      <form class="form-inline my-2 my-lg-0">
        <input class="form-control mr-sm-2" type="search" placeholder="O que procura?" aria-label="Buscar">
        <button class="btn btn-outline-primary my-2 my-sm-0" type="submit">Buscar</button>
      </form>
    </div>
  </nav>
</template>

<script>
  export default {
    name: 'BNavBar',
  }
</script>

