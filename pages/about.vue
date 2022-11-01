<template>
  <div>
    <section class="about">
      <div class="container">
        <div class="section-title" data-aos="fade-down">
          <h1>About</h1>
        </div>
        <div class="row">
          <div class="col-lg-3 text-center" data-aos="fade-right">
            <img src="/images/ponlapat.jpg" alt="Ponlapat Ittiratchapong" class="img-responsive"/>
          </div>
          <div class="col-lg-9 content" data-aos="fade-left">
            <h3>Software Engineer & Cyber Security</h3>
            <p>Hello! My name is Ponlapat Ittiratchapong, I'm living in Thailand. Currently I'm studying Software Engineering (Year 3) at Thammasat University. Now I'm looking to be full-stack developer and also I'm interested in Cyber Security too.</p>
            <div class="row">
              <div class="col-md-6">
                <ul>
                  <li><i class="fa-solid fa-user fa-fw"></i> <b>Age: </b> 20</li>
                  <li><i class="fa-solid fa-house fa-fw"></i> <b>Website: </b> <a href="https://mrthebank.github.io">mrthebank.github.io</a></li>
                  <li><i class="fa-sharp fa-solid fa-graduation-cap"></i> <b>Degree: </b> Undergraduate</li>
                  <li><i class="fa-brands fa-linkedin fa-fw"></i> <b>LinkedIn: </b> <a href="https://www.linkedin.com/in/ponlapat-ittiratchapong/">bit.ly/3CCNvmi</a></li>
                </ul>
              </div>
              <div class="col-md-6">
                <ul>
                  <li><i class="fa-solid fa-location-dot fa-fw"></i> <b>Locate: </b> Pathum Thani, Thailand</li>
                  <li><i class="fa-solid fa-envelope fa-fw"></i> <b>Email: </b> ponlapat.itt@gmail.com</li>
                  <li><i class="fa-solid fa-building-columns fa-fw"></i> <b>University: </b> Thammasat University</li>
                  <li><i class="fa-brands fa-github fa-fw"></i> <b>GitHub: </b> <a href="https://github.com/MrTheBank">github.com/MrTheBank</a></li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="skills">
      <div class="container">
        <div class="section-title" data-aos="fade-down">
          <h1>Skills</h1>
        </div>
        <div class="row g-4" data-aos="zoom-in">
          <div class="col-sm-6 col-md-4 col-lg-3 col-xl-2" v-for="s in skills" data-aos="fade-right">
            <div class="box-content">
              <img :src="s.icon" :alt="s.name"/>
              <div class="box-text">{{ s.name }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="interests">
      <div class="container">
        <div class="section-title" data-aos="fade-down">
          <h1>Interests</h1>
        </div>
        <div class="row g-4" data-aos="zoom-in">
          <div class="col-md-6 col-lg-4 col-xl-3" v-for="i in interests" data-aos="fade-right">
            <div class="box-content">
              <img :src="i.icon" :alt="i.name"/>
              <div class="box-text">{{ i.name }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import AOS from "aos";

export default {
  name: "about",
  head() {
    return {
      title: 'About Me'
    }
  },
  data() {
    return {
      skills: [],
      interests: []
    }
  },
  mounted() {
    AOS.init({
      duration: 800,
      easing: 'ease-in-out',
    });

    this.getAboutAPI();
  },
  methods: {
    async getAboutAPI() {
      let res = (await this.$axios.get('https://mrthebank.github.io/mrthebank.github.io-api/about.json')).data;

      this.skills = res.skills;
      this.interests = res.interests;
    }
  }
}
</script>

<style scoped>
.about {
  padding: 45px 0;
}
.about .content p {
  font-size: 1.25rem;
  margin-bottom: 1rem;
}
.about .content ul {
  list-style: none;
  padding: 0;
}
.about .content ul > li {
  font-size: 1.25rem;
  margin-bottom: 10px;
}
.about .content ul > li b {
  font-weight: 500;
}
.about .content ul > li a {
  color: #4f4f4f;
}
.skills {
  padding: 45px 0;
}
.skills .box-content {
  align-items: center;
  display: flex;
  background: #ECF0F1;
  height: 50px;
  border-radius: 10px;
  justify-content: space-evenly;
}
.skills .box-content img {
  height: 30px;
}
.skills .box-content .box-text {
  color: #0d0d0d;
  font-size: 1.25rem;
  font-weight: 400;
}
.interests {
  padding: 45px 0;
}
.interests .box-content {
  align-items: center;
  display: flex;
  background: #ECF0F1;
  height: 80px;
  border-radius: 10px;
  justify-content: space-evenly;
}
.interests .box-content img {
  height: 40px;
}
.interests .box-content .box-text {
  color: #0d0d0d;
  font-size: 1.5rem;
  font-weight: 500;
}
.img-responsive {
  width: 100%;
}
@media screen and (max-width: 992px) {
  .img-responsive {
    width: 75%;
  }
  .about .content h3 {
    text-align: center;
    margin-top: 0.5rem;
  }
}
</style>
