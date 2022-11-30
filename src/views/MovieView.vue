<template>
  <div>
    <HeaderCont />
    <TitleCont name1="movie" name2="reference api" />
    <section className="cont__refer">
      <div className="container">
        <div className="movie__inner">
          <!-- movie__slider -->
          <div class="movie__slider">
            <swiper
              :effect="'coverflow'"
              :grabCursor="true"
              :centeredSlides="true"
              :slidesPerView="'auto'"
              :initialSlide="3"
              :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: true,
              }"
              :pagination="true"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="slider in sliders" :key="slider.id">
                <a :href="`https://image.tmdb.org/movie/${slider.id}`">
                  <img
                    :src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
                    :alt="slider.title"
                  />
                  <!-- <p>{{ slider.title }}</p> -->
                  <!-- <div class="content__desc">
                    <p>{{ slider.vote_average }}</p>
                    <p>{{ slider.original_language }}</p>
                  </div> -->
                </a>
              </swiper-slide>
            </swiper>
          </div>
          <!-- movie__search -->f
          <div className="movie__search">
            <div className="container">
              <form @submit.prevent="SearchMovies()">
                <input
                  id="search"
                  type="search"
                  placeholder="검색하세요!"
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
            </div>
          </div>
          <!-- movie__movies" -->
          <div class="movie__movies">
            <div class="container">
              <div class="movie__list">
                <ul>
                  <li v-for="movie in movies" :key="movie.id">
                    <a href="#">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                        :alt="movie.title"
                      />
                    </a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import "swiper/css";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
import { EffectCoverflow, Pagination } from "swiper";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref("marvel");

    // const PopularMovie = async () => {
    //   await fetch(
    //     `https://api.themoviedb.org/3/movie/popular?api_key=3d606cf9dc17d29e0dec9772c8a629e6&`
    //   )
    //     .then((response) => response.json())
    //     .then((result) => (sliders.value = result.results))
    //     .catch((error) => console.log(error));
    // };
    // PopularMovie();

    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=3d606cf9dc17d29e0dec9772c8a629e6&query=${search.value}`
      )
        .then((response) => response.json())
        .then((result) => {
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchMovies();

    const TopMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=3d606cf9dc17d29e0dec9772c8a629e6&`
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log(error));
    };
    TopMovies();

    return {
      movies,
      sliders,
      search,
      TopMovies,
      SearchMovies,
      modules: [EffectCoverflow, Pagination],
    };
  },
};
</script>

<style lang="scss">
.movie__list {
  ul {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    li {
      width: 19%;
      margin-bottom: 2%;
    }
  }
}

// movieSearch

.movie__search {
  margin-bottom: 100px;

  .container {
    position: relative;
  }

  h2 {
    color: var(--black);
    font-size: 40px;
    text-indent: -9999px;
    height: 0;
  }
  input {
    background: #eee;
    border: 1px solid #d0d0d0;
    border-radius: 50px;
    color: var(--black);
    width: 100%;
    padding: 14px 30px;
    font-family: var(--font-kor);
    margin-top: 20px;
  }
  button {
    position: absolute;
    right: 6px;
    top: 5px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 0;
    cursor: pointer;
    z-index: 1000;
    margin-top: 20px;
    background: var(--white);
  }
}

// swiper
.swiper {
  width: 100% !important;
  padding-top: 50px;
  padding-bottom: 50px;
  height: auto !important;
}

.swiper-slide {
  background-position: center;
  background-size: cover;
  width: 300px;
  height: 450px;
}

.swiper-slide img {
  display: block;
  width: 100%;
  box-shadow: 0px 20px 40px -15px #000000bd;
}

.content__desc {
  position: absolute;
  bottom: 10px;
  right: 10px;
  background: #000;
  display: flex;
  color: #fff;
  border-radius: 5px;
  /* width: 50px; */
  /* height: 50px; */
  padding: 10px;
}
.content__desc p:nth-child(1) {
  padding-right: 10px;
  margin-right: 10px;
  border-right: 1px solid #ffffff4a;
}
</style>
