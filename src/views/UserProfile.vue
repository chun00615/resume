<template>
  <div class="profile">
    <div class="tabs">
      <ul class="tabs--list">
        <li v-for="(tab, index) in tabs" :key="index">
          <a href="javascript:;" :title="tabsName[index]" :class="{ 'actived': activeTab === index }"
            @click="changeTab(index)">
            {{ tab }}
          </a>
        </li>
        <li class="moving-tab moving-tab--interaction" :style="movingTabStyle"></li>
      </ul>

    </div>

    <div class="container">
      <div class="slider-custom-buttons">
        <button class="swiper-custom-button-prev" @click="swiperPrev">
          <span class="material-icons">arrow_back</span>
        </button>
        <button class="swiper-custom-button-next" @click="swiperNext">
          <span class="material-icons">arrow_forward</span>
        </button>
      </div>
      <swiper class="profileSwiper" :modules="modules" :speed="600" :navigation="false" :pagination="{
        dynamicBullets: true,
      }" :hashNavigation="{
  watchState: true,
}">

        <!-- <div class="parallax-bg" data-swiper-parallax="-23%"></div> -->
        <swiper-slide data-hash="home">
          <HomeSection data-swiper-parallax="-300" />
        </swiper-slide>
        <swiper-slide data-hash="aboutMe">
          <AboutMe data-swiper-parallax="-200" />
        </swiper-slide>
        <swiper-slide data-hash="advantage">
          <AdvantageSection data-swiper-parallax="-100" />
        </swiper-slide>
        <swiper-slide data-hash="experience">
          <ExperienceSection />
        </swiper-slide>
      </swiper>
    </div>


  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
// ,Pagination
import 'swiper/swiper-bundle.css';
// import SwiperCore, { Mousewheel, Pagination } from "swiper";
// import "swiper/swiper.min.css";

// import "swiper/modules/pagination.min.css";

// import "swiper/modules/navigation/navigation.min.css";
import HomeSection from '@/components/HomeSection.vue';
import AboutMe from '@/components/AboutMe.vue';
import AdvantageSection from '@/components/AdvantageSection.vue';
import ExperienceSection from '@/components/ExperienceSection.vue';

import { Navigation, Pagination, Scrollbar, A11y, Parallax, HashNavigation } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/pagination';
import 'swiper/css/scrollbar';
export default {
  components: {
    Swiper,
    SwiperSlide,
    HomeSection,
    AboutMe,
    AdvantageSection,
    ExperienceSection,
  },
  setup() {

    const swiperPrev = () => {
      activeTab.value -= 1;
      const swiper = document.querySelector('.profileSwiper').swiper;
      if (swiper) {
        swiper.slidePrev();
      }
    };

    const swiperNext = () => {
      activeTab.value += 1;
      const swiper = document.querySelector('.profileSwiper').swiper;
      if (swiper) {
        swiper.slideNext();
      }
    };

    const tabs = ['home', 'aboutMe', 'advantage', 'experience'];
    const tabsName = ['Home', 'About Me', 'Advantage', 'Experience'];

    const activeTab = ref(0);
    const detectHashAndSetTab = () => {
      const hash = window.location.hash.slice(1);
      const index = tabs.indexOf(hash);
      if (index !== -1) {
        activeTab.value = index;
      }
    };

    onMounted(() => {
      detectHashAndSetTab();
      window.addEventListener('hashchange', detectHashAndSetTab);
    });


    const changeTab = (index) => {
      activeTab.value = index;
      window.location.hash = tabs[index];
    };

    const movingTabStyle = computed(() => {
      const howFar = 28 * activeTab.value - 8;
      return {
        left: howFar + '%',
      };
    });

    return {
      tabs,
      tabsName,
      activeTab,
      movingTabStyle,
      modules: [Navigation, Pagination, Scrollbar, A11y, Parallax, HashNavigation],
      changeTab,
      swiperPrev,
      swiperNext
    };
  },
};
</script>

<style lang="scss">
@import "./UserProfile.scss";
</style>