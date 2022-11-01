<template>
  <nav class="navbar navbar-expand-md navbar-dark nav-portfolio">
    <div class="container-fluid">
      <div class="logo">
        <a href="">Ponlapat</a>
      </div>
      <div class="social-button ms-auto">
        <a href="mailto:ponlapat.itt@dome.tu.ac.th"><i class="fa-solid fa-envelope"></i></a>
        <a href="https://www.linkedin.com/in/ponlapat-ittiratchapong-842586219" target="_blank"><i class="fa-brands fa-linkedin"></i></a>
        <a href="https://github.com/MrTheBank" target="_blank"><i class="fa-brands fa-github"></i></a>

        <button class="navbar-toggler" type="button" data-mdb-toggle="collapse" data-mdb-target="#navbarPortfolio" aria-controls="navbarPortfolio" aria-expanded="false" aria-label="Toggle navigation">
          <i class="fa-solid fa-bars"></i>
        </button>
      </div>

      <div class="collapse navbar-collapse justify-content-center" id="navbarPortfolio">
        <ul class="navbar-nav mb-2 mb-lg-0">
          <li class="nav-item">
            <NuxtLink class="nav-link" to="/">Home</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" to="/about">About</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" to="/portfolio">Portfolio</NuxtLink>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="https://mrthebank.github.io/mrthebank.github.io-api/Ponlapat%20Resume.pdf" target="_blank">Resume</a>
          </li>
        </ul>
      </div>
      <div class="social-button-md text-end">
        <a href="mailto:ponlapat.itt@gmail.com"><i class="fa-solid fa-envelope"></i></a>
        <a href="https://www.linkedin.com/in/ponlapat-ittiratchapong-842586219" target="_blank"><i class="fa-brands fa-linkedin"></i></a>
        <a href="https://github.com/MrTheBank" target="_blank"><i class="fa-brands fa-github"></i></a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Header"
}
</script>

<style scoped>
.nav-portfolio {
  background-color: #0d0d0d;
  min-height: 50px;
}
.navbar .logo {
  width: 120px;
}
.navbar .logo a {
  text-transform: uppercase;
  font-size: 20px;
  font-weight: 300;
  letter-spacing: 2px;
  color: rgba(255, 255, 255, 0.75);
}
.navbar .nav-item a {
  font-size: 15px;
}
.navbar .social-button > a, .navbar .social-button-md > a {
  color: rgba(255, 255, 255, 0.55);
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out;
  padding-left: 2px;
}
.navbar .social-button > a:hover, .navbar .social-button-md > a:hover {
  color: rgba(255, 255, 255, 0.75);
}
.navbar .social-button > a > i, .navbar .social-button-md > a > i {
  padding: 0.25rem;
  font-size: 1.25rem;
}
.navbar a:hover:before, .navbar .active:before {
  visibility: visible !important;
  width: 40px !important;
}
.navbar .navbar-nav > .nav-item > a:before {
  content: "";
  position: absolute;
  width: 0;
  height: 2px;
  bottom: 4px;
  left: 0;
  background-color: rgba(255, 255, 255, 0.75);
  visibility: hidden;
  transition: all 0.3s ease-in-out 0s;
}
.navbar .navbar-nav > .nav-item > .active:before {
  background-color: #fff !important;
}
.navbar a, .navbar a:focus {
  position: relative;
}
.navbar .social-button-md {
  display: none;
}
.navbar .logout {
  display: block;
}
@media screen and (min-width: 768px) {
  .nav-portfolio {
    height: 50px;
  }
  .navbar .social-button {
    display: none;
  }
  .navbar .social-button-md {
    width: 120px;
    display: block;
  }
  .navbar a:hover:before, .navbar .active:before {
    width: calc(100% - 1rem) !important;
  }
  .navbar .navbar-nav > .nav-item > a:before {
    left: 8px;
  }
  .navbar .logout {
    display: none;
  }
}

</style>
