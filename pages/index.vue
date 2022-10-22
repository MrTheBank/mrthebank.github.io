<template>
  <div>
    <client-only>
      <Particles id="tsparticles" :particlesInit="particlesInit" :options="particle"/>
    </client-only>
    <div class="d-flex align-items-center justify-content-center home-full-height">
      <div class="text-center">
        <h1 class="home-title display-3">
          <MyName/>
        </h1>
        <h2 class="home-subtitle display-6">
          <MyPosition/>
        </h2>
        <div class="home-button">
          <NuxtLink class="btn btn-outline-light btn-xlg btn-rounded" to="/about">About Me</NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { loadFull } from "tsparticles";

import particle from "../assets/home_tsparticles.json";

export default {
  name: 'Home',
  head() {
    return {
      title: 'Home'
    }
  },
  data() {
    return {
      particle: particle
    }
  },
  methods: {
    async particlesInit(engine) {
      return await loadFull(engine);
    }
  }
}
</script>

<style>
.home-full-height {
  min-height: calc(100vh - 50px);
}
.home-title {
  color: #ffffff;
  font-weight: 400;
}
.home-subtitle {
  color: #e6e6e6;
}
.text-thammasat {
  color: #ffd13f;
}
.text-university {
  color: #c3002f;
}
.home-button {
  margin-top: 40px;
}
.btn-xlg {
  padding: 0.85rem 2rem 0.85rem 2rem !important;
}
</style>
