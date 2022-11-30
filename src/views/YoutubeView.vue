<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Youtube" name2="reference" />
    <section class="cont__refer">
      <div class="container">
        <div class="youtube__inner">
          <div class="youtube__slider">
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
              <swiper-slide v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img
                    :src="splash.snippet.thumbnails.medium.url"
                    :alt="splash.snippet.thumbnails.medium.url"
                  />
                  <!-- <p>{{ splash.snippet.title }}</p> -->
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
            </div>
          </div>
          <div class="youtube__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.snippet.channelTitle">
                <a href="#">
                  <img
                    :src="splash.snippet.thumbnails.medium.url"
                    :alt="splash.snippet.channelTitle"
                  />
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
        // `https://youtube.googleapis.com/youtube/v3/search?key=AIzaSyAp7wwVT_hzfA2mSXrrh-1ZUx7QCX3ogtk&part=snippet&maxResults=10&type=video&q=${search.value}`
        `https://raw.githubusercontent.com/younghwan12/reactapi/main/src/utils/youtube.json`
      )
        .then((response) => response.json())
        .then((result) => {
          splashes.value = result.items;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchSplashes();

    const RandomSplashes = () => {
      fetch(
        `https://raw.githubusercontent.com/younghwan12/reactapi/main/src/utils/youtube.json`
      )
        .then((response) => response.json())
        .then((result) => (splashes.value = result.items))
        .then((result) => console.log(result))
        .catch((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      SearchSplashes,
      RandomSplashes,
      modules: [EffectCoverflow, Pagination],
    };
  },
};
</script>

<style lang="scss">
.youtube__images {
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

.swiper {
  width: 100% !important;
  height: 100% !important;
}

.swiper-slide {
  background-position: center !important;
  background-size: cover !important;
}

.swiper-slide img {
  display: block !important;
  width: 100% !important;
}
.youtube__slider .swiper-slide {
  width: auto;
  height: auto;
  display: auto;
  box-shadow: auto;
}
.youtube__slider .swiper-slide img {
  box-shadow: 0px 1px 40px -15px rgb(0 0 0 / 20%);
}
</style>
