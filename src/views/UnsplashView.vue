<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Unsplash" name2="reference" />
    <section class="cont__refer">
      <div class="container">
        <div class="unsplash__inner">
          <div class="unsplash__slider">
            <swiper
              :effect="'cards'"
              :grabCursor="true"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                  <p>{{ splash.likes }}</p>
                </a>
              </swiper-slide>
            </swiper>
          </div>
          <div class="movie__search">
            <div className="container">
              <form @submit.prevent="SearchSplashes()">
                <input
                  id="search"
                  type="search"
                  placeholder="검색하세요!"
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
              <!-- <button
                v-for="title in titles"
                :key="title.text"
                :value="title.text"
                v-on:click="TagSearchSplashes()"
              >
                {{ title.text }}
              </button> -->
            </div>
          </div>
          <div class="unsplash__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
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

// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";

import "swiper/css/effect-cards";

// import "./style.css";

// import required modules
import { EffectCards } from "swiper";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },
  data: function () {
    return {
      titles: [
        { text: "bike" },
        { text: "tiger" },
        { text: "guitar" },
        { text: "car" },
      ],
    };
  },

  setup() {
    const splashes = ref([]);
    const search = ref("landscape");

    const SearchSplashes = async () => {
      await fetch(
        `https://api.unsplash.com/search/photos?page=1&query=${search.value}&client_id=7q3_gZMO4lwUgeFywj-wLxCLnDs2ldqIsoZ0iPeiJu0&count=15`
      )
        .then((response) => response.json())
        .then((result) => {
          splashes.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchSplashes();

    const TagSearchSplashes = async () => {
      await fetch(
        `https://api.unsplash.com/search/photos?page=1&query=${search.value}&client_id=7q3_gZMO4lwUgeFywj-wLxCLnDs2ldqIsoZ0iPeiJu0&count=15`
      )
        .then((response) => response.json())
        .then((result) => {
          splashes.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchSplashes();

    const RandomSplashes = () => {
      fetch(
        `https://api.unsplash.com/photos/random?page=1&query=office&client_id=7q3_gZMO4lwUgeFywj-wLxCLnDs2ldqIsoZ0iPeiJu0&count=15`
      )
        .then((response) => response.json())
        .then((result) => (splashes.value = result))
        .then((result) => console.log(result))
        .catch((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      SearchSplashes,
      TagSearchSplashes,
      RandomSplashes,
      modules: [EffectCards],
    };
  },
};
</script>

<style lang="scss">
.unsplash__images {
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
.unsplash__slider {
  width: 680px;
  margin: 0 auto;
}
.unsplash__images li {
  text-align: center;
  margin-bottom: 20px;
}
.unsplash__images li a img {
  height: 100%;
  object-fit: cover;
}

.swiper {
  width: 675px;
  height: 320px;
}

.swiper-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 18px;
  font-size: 22px;
  font-weight: bold;
  color: #fff;
  box-shadow: 0px 20px 20px -10px #0e0e0d57;
  position: relative;
  p {
    position: absolute;
    bottom: 10px;
    right: 10px;
    color: #fff;
    &::before {
      position: absolute;
      bottom: 26px;
      right: 10px;
      content: "♥︎";
      color: #ff1f50;
    }
  }
}

.swiper-slide:nth-child(1n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(2n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(3n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(4n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(5n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(6n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(7n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(8n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(9n) {
  background-color: #3c3c3c;
}

.swiper-slide:nth-child(10n) {
  background-color: #3c3c3c;
}
</style>
