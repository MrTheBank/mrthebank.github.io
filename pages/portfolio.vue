<template>
  <div>
    <section class="portfolio">
      <div class="container">
        <div class="section-title" data-aos="fade-down">
          <h1>Portfolio</h1>
          <p>This is my portfolio that shows my projects that I have built or competitions that I have attended.</p>
        </div>
        <div data-aos="fade-down">
          <ul class="filter">
            <li :class="activeFilter('all')" @click="changeFilter('all')">All</li>
            <template v-for="c in categories">
              <li :class="activeFilter(c.id)" @click="changeFilter(c.id)">{{ c.name }}</li>
            </template>
          </ul>
        </div>
          <no-ssr>
            <isotope ref="cpt" class="row g-4" :options='getOptions()' :list="portfolios" v-images-loaded:on.progress="layout">
              <div class="col-lg-4 col-md-6 portfolio-item" v-for="(p, index) in portfolios" :key="index">
                <div class="portfolio-wrap">
                  <img :src="p.img_url" class="img-fluid">
                  <div class="portfolio-info">
                    <h4>{{ p.title }}</h4>
                    <p>{{ categories.filter(c => c.id === p.category)[0].name }}</p>
                    <div class="portfolio-links">
                      <a href="#" class="portfolio-lightbox" @click="openModal(index)"><i class="fa-solid fa-plus fa-xs"></i></a>
                      <a :href="p.url" :target="p.url === '#' ? '' : '_blank'" class="portfolio-details-lightbox"><i class="fa-solid fa-link fa-xs"></i></a>
                    </div>
                  </div>
                </div>
              </div>
            </isotope>
          </no-ssr>
      </div>
    </section>
    <div class="modal fade" ref="PortfolioModel" tabIndex="-1" aria-hidden="true">
      <div class="modal-dialog modal-xl">
        <div class="modal-content">
          <div class="modal-header">
            <h4 class="modal-title">{{ modalInfo.title }}</h4>
            <button type="button" class="btn-close" data-mdb-dismiss="modal" aria-label="Close"/>
          </div>
          <div class="modal-body">
            <div id="carouselIndicators" class="carousel slide" data-mdb-ride="carousel">
              <div class="carousel-indicators">
                <template v-for="(i, index) in modalInfo.gallery">
                  <button
                    type="button"
                    data-mdb-target="#carouselIndicators"
                    :data-mdb-slide-to="index"
                    :class="index === 0 ? 'active' : ''"
                  ></button>
                </template>
              </div>
              <div class="carousel-inner">
                <template v-for="(i, index) in modalInfo.gallery">
                  <div :class="'carousel-item' + (index === 0 ? ' active' : '')">
                    <img :src="i" class="d-block w-100" :alt="modalInfo.title"/>
                  </div>
                </template>
              </div>
              <button class="carousel-control-prev" type="button" data-mdb-target="#carouselIndicators" data-mdb-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
              </button>
              <button class="carousel-control-next" type="button" data-mdb-target="#carouselIndicators" data-mdb-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
              </button>
            </div>
            <div class="mt-2" v-html="modalInfo.description">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AOS from "aos";

export default {
  name: "portfolio",
  head() {
    return {
      title: 'Portfolio'
    }
  },
  data() {
    return {
      filter: 'all',
      categories: [],
      portfolios: [],
      modalInfo: {
        title: '',
        gallery: [],
        description: ''
      },

      modal: null
    }
  },
  mounted() {
    AOS.init({
      duration: 800,
      easing: 'ease-in-out',
    });

    this.modal = new this.$mdb.Modal(this.$refs.PortfolioModel);

    this.getPortfolioAPI();
  },
  methods: {
    async getPortfolioAPI() {
      let res = (await this.$axios.get('https://mrthebank.github.io/mrthebank.github.io-api/portfolio.json')).data;

      this.categories = res.categories;
      this.portfolios = res.portfolios;
    },
    getOptions() {
      let _this = this;
      return {
        itemSelector: '.portfolio-item',
        getFilterData: {
          filter(itemElem) {
            return itemElem.category === _this.filter;
          }
        }
      }
    },
    activeFilter(id) {
      return this.filter === id ? 'filter-active' : '';
    },
    changeFilter(id) {
      this.filter = id;

      if (id === 'all') {
        return this.$refs.cpt.unfilter();
      } else {
        return this.$refs.cpt.filter('filter');
      }
    },
    layout() {
      return this.$refs.cpt.layout('masonry');
    },
    openModal(index) {
      let data = this.portfolios[index];
      this.modalInfo.title = data.title;
      this.modalInfo.gallery = data.gallery;
      this.modalInfo.description = data.description;

      return this.modal.show();
    }
  }
}
</script>

<style scoped>
.portfolio {
  padding: 45px 0;
}
.portfolio .filter {
  padding: 0;
  margin: 0 auto 20px auto;
  list-style: none;
  text-align: center;
}
.portfolio .filter li.filter-active, .portfolio .filter li:hover {
  color: #fff;
  background: #0099ff;
}
.portfolio .filter li {
  cursor: pointer;
  display: inline-block;
  padding: 8px 16px 10px 16px;
  font-size: 13px;
  font-weight: 500;
  line-height: 1;
  text-transform: uppercase;
  color: #444444;
  margin-bottom: 5px;
  margin-right: 4px;
  transition: all 0.3s ease-in-out;
  border-radius: 50px;
}

.portfolio .portfolio-wrap {
  transition: 0.3s;
  position: relative;
  overflow: hidden;
  z-index: 1;
  background: rgba(34, 34, 34, 0.6);
}

.portfolio .portfolio-wrap::before {
  content: "";
  background: rgba(34, 34, 34, 0.6);
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  transition: all ease-in-out 0.3s;
  z-index: 2;
  opacity: 0;
}

.portfolio .portfolio-wrap img {
  transition: all ease-in-out 0.3s;
}

.portfolio .portfolio-wrap .portfolio-info {
  opacity: 0;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 3;
  transition: all ease-in-out 0.3s;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: flex-start;
  padding: 20px;
}

.portfolio .portfolio-wrap .portfolio-info h4 {
  font-size: 20px;
  color: #fff;
  font-weight: 400;
}

.portfolio .portfolio-wrap .portfolio-info p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 14px;
  text-transform: uppercase;
  padding: 0;
  margin: 0;
  font-style: italic;
}

.portfolio .portfolio-wrap .portfolio-links {
  text-align: center;
  z-index: 4;
}

.portfolio .portfolio-wrap .portfolio-links a {
  color: #fff;
  margin: 0 5px 0 0;
  font-size: 28px;
  display: inline-block;
  transition: 0.3s;
}

.portfolio .portfolio-wrap .portfolio-links a:hover {
  color: #78d9cd;
}

.portfolio .portfolio-wrap:hover::before {
  opacity: 1;
}

.portfolio .portfolio-wrap:hover img {
  transform: scale(1.2);
}

.portfolio .portfolio-wrap:hover .portfolio-info {
  opacity: 1;
}
</style>
