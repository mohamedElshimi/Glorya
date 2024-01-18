<template>
  <!-- <header class="py-3 position-relative">
        <div
            :class="`container d-flex align-items-center justify-content-between gap-4 ${router.currentRoute.value.path !== `/${$i18n.locale}` ? 'not-home' : ''}`">
            <div class="logo">
                <router-link class="text-decoration-none" :to="`/${$i18n.locale}`">
                    <img :src="`https://seasonreal.seasonsge.com/${info.logo}`" alt="">
                </router-link>
            </div>
            <ul :class="`links d-flex align-items-center justify-content-between gap-5 w-100 ${openMenu ? 'open' : ''}`">
                <ul class="d-flex align-items-center gap-5 flex-lg-row flex-column">
                    <li v-for="(item, index) in $tm('headerLinks')" :key="index">
                        <a v-if="router.currentRoute.value.path === `/${$i18n.locale}` && (item === 'about' || item === 'عنا')"
                            class="text-decoration-none fw-bold text-muted text-capitalize fs-5"
                            :href="`#${item === 'about' || 'عنا' ? 'about' : ''}`">
                            {{ item }}
                        </a>
                        <router-link v-else class="text-decoration-none fw-bold text-muted text-capitalize fs-5"
                            :to="`${item === 'programmes' || item === 'برامجنا' ? `/${$i18n.locale}/programmes`
                                : item === 'contact' || item === 'تواصل معنا' ? `/${$i18n.locale}/contact` : `/${$i18n.locale}`}`">
                            {{ item }}
                        </router-link>
                    </li>
                </ul>
                <div class="d-flex align-items-center gap-3 flex-lg-row flex-column">
                    <router-link v-if="Object.keys(userInfo).length === 0"
                        class="agent-button text-uppercase text-decoration-none butn p-2 px-3 rounded-1 text-nowrap"
                        :to="`/${$i18n.locale}/client-login`">
                        {{ $t('buttons.login') }}
                    </router-link>
                    <span class="lang fw-bold d-flex align-items-center gap-2" @click="changeLang">
                        <i class="fa-solid fa-globe fs-4"></i>
                        {{ $i18n.locale === 'en' ? 'AR' : 'EN' }}
                    </span>
                </div>
            </ul>
            <div v-if="Object.keys(userInfo).length > 0" type="button" @click="openAccountBox = !openAccountBox"
                class="account position-relative text-black fw-bold d-flex align-items-center gap-2 ms-auto text-decoration-none">
                <img width="50" height="50" style="object-fit: cover;" class="rounded-circle"
                    :src="`https://seasonreal.seasonsge.com/images/Agents/${userInfo.img}`" alt="">
                <i class="fa-solid fa-chevron-down"></i>

                <div v-if="openAccountBox" class="box rounded-2 d-flex flex-column bg-white">
                    <router-link class="d-flex align-items-center text-decoration-none text-black gap-3 p-2 px-4"
                        :to="{ name: 'Client Account', params: { lang: $i18n.locale } }">
                        <i class="fa-solid fa-user"></i>
                        Account
                    </router-link>
                    <button @click="logOut"
                        class="bg-transparent border-0 d-flex align-items-center fw-bold text-decoration-none text-danger gap-3 p-2 px-4"
                        to="/">
                        <i class="fa-solid fa-arrow-right-from-bracket"></i>
                        Logout
                    </button>
                </div>

            </div>
            <i :class="`fa-solid fa-bars fs-2 menu ${openMenu ? 'open' : ''}`" @click="openMenu = true"></i>
            <i :class="`fa-solid fa-xmark fs-2 close ${openMenu ? 'open' : ''}`" @click="openMenu = false"></i>
        </div>
    </header> -->
  <header class="w-full d-flex flex-wrap">
    <div class="min-h-60 w-100 bg-gray-200 d-sm-block d-none">
      <div
        class="col-11 mx-auto d-flex flex-wrap justify-content-between align-items-center h-100 pt-3"
      >
        <div class="d-flex gap-1 align-items-center mb-3">
          <i class="fa-solid fa-calendar main-color"></i>
          <span class="me-3 fs-6"
            >{{ $t(`date.days[${currentDay}]`) }} , {{ currentNumOfDay }}
            {{ $t(`date.months[${currentMonth}]`) }} , {{ currentYear }}</span
          >
        </div>
        <marquee
          :direction="$i18n.locale === 'en' ? 'left' : 'right'"
          behavior="scroll"
          scrollamount="8"
          class="mb-3 col-lg-5 col-md-6"
        >
          {{ $t("header.marqueePara") }}
        </marquee>
        <div class="d-flex col-lg-4 col-md-6 gap-1 align-items-center mb-3">
          <span
            class="bg-light text-black px-2 p-1 rounded-3 d-flex align-items-center me-3"
          >
            <i class="fa-solid fa-sun ms-1 main-color"></i>
            <span class="ms-2">{{ temp }} C</span>
          </span>
          <router-link
            :to="`/${$i18n.locale}/client-login`"
            class="bg-main-color text-white px-2 p-1 rounded-3 d-flex align-items-center me-3"
          >
            <i class="fa-solid fa-user fs-6 ms-1"></i>
            <span class="ms-2">{{ $t("header.login") }}</span>
          </router-link>
          <span
            class="lang btn btn-light fw-bold d-flex align-items-center gap-2 me-2"
            @click="changeLang"
          >
            <i class="fa-solid fa-globe fs-4"></i>
            {{ $i18n.locale === "en" ? "AR" : "EN" }}
          </span>
        </div>
      </div>
    </div>
    <div
      class="h-[250px] w-100 overflow-hidden relative"
      v-if="isRouteActive('/ar') || isRouteActive('/en')"
    >
      <swiper
        :modules="modules"
        :slides-per-view="1"
        :loop="true"
        :autoplay="{
          delay: 1000,
          diableOnInteraction: false,
          pauseOnMouseEnter: true,
        }"
        :space-between="0"
        @swiper="onSwiper"
        @slideChange="onSlideChange"
        class="w-100 d-flex justify-content-center"
      >
        <swiper-slide
          ><img
            src="../../public/images/Banner.jpeg"
            alt="Home Banner"
            class="top-50 -translate-y-1/2 w-100 h-100"
        /></swiper-slide>
        <swiper-slide
          ><img
            src="../../public/images/Banner.jpeg"
            alt="Home Banner"
            class="top-50 -translate-y-1/2 w-100 h-100"
        /></swiper-slide>
        <swiper-slide
          ><img
            src="../../public/images/Banner.jpeg"
            alt="Home Banner"
            class="top-50 -translate-y-1/2 w-100 h-100"
        /></swiper-slide>
      </swiper>
    </div>
    <nav
      class="navbar navbar-expand-lg bg-body-tertiary w-100 order-first order-sm-0"
    >
      <div class="container">
        <router-link
          class="navbar-brand me-0 me-md-auto ms-4"
          :to="`/${$i18n.locale}`"
          ><img src="../../public/images/logo.png" alt="" height="60"
        /></router-link>
        <span
          class="lang btn btn-dark me-auto fw-bold d-flex align-items-center gap-2 ms-3 d-sm-none d-block"
          @click="changeLang"
        >
          <i class="fa-solid fa-globe fs-4"></i>
          {{ $i18n.locale === "en" ? "AR" : "EN" }}
        </span>
        <button
          class="navbar-toggler order-md-first"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item position-relative">
              <router-link
                :to="`/${$i18n.locale}`"
                class="nav-link fw-semibold"
                aria-current="page"
                :class="{
                  active: isRouteActive('/ar') || isRouteActive('/en'),
                }"
                ><i class="fa-solid fa-house ms-2"></i
                >{{ $t("header.links.li1") }}</router-link
              >
            </li>
            <template
              v-for="(item, index) in $tm('serviciesCards')"
              :key="index"
            >
              <li class="nav-item position-relative">
                <router-link
                  v-if="!item.link.includes('http')"
                  class="nav-link fw-semibold"
                  :to="`/${$i18n.locale}/${item.link}`"
                  :class="{
                    active:
                      isRouteActive(`/ar/${item.link}`) ||
                      isRouteActive(`/en/${item.link}`),
                  }"
                >
                  <i class="fa-solid fa-shield ms-2" v-if="index == 0"></i>
                  <i class="fa-solid fa-hotel ms-2" v-else-if="index == 1"></i>
                  <i
                    class="fa-solid fa-car-side ms-2"
                    v-else-if="index == 2"
                  ></i>
                  <i class="fa-sharp fa-solid fa-train ms-2" v-else></i>
                  {{ item.heading }}
                </router-link>
                <a
                  v-if="item.link.includes('http')"
                  target="_blank"
                  class="fw-bold nav-link"
                  :href="item.link"
                >
                  <i class="fa-sharp fa-solid fa-train ms-2"></i>
                  {{ item.heading }}
                </a>
              </li>
            </template>
            <li class="nav-item position-relative">
              <router-link
                :to="`/${$i18n.locale}/contactUs`"
                class="nav-link fw-semibold"
                aria-current="page"
                :class="{
                  active: isRouteActive('/ar/contactUs') || isRouteActive('/en/contactUs'),
                }"
                ><i class="fa-solid fa-message mx-2"></i>{{ $t("header.links.li2") }}</router-link
              >
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <!-- <div class="min-h-[70px] w-full shadow-md lg:order-none order-first">
            <div class="lg:w-10/12 md:w-11/12 px-7 mx-auto flex flex-wrap items-center h-full justify-between">
                <div class="h-[70px] me-5 mx-auto py-2">
                    <img src="../../public/images/sky-logo.png" class="h-full" alt="">
                </div>
                <nav class="me-auto lg:w-10/12 w-2/12 lg:order-none order-first h-full flex items-center">
                    <button class="resposive-icon px-3 py-2 text-black bg-secondry-1 hidden text-2xl" @click="toggleMenuBar" v-if="!menubarOpen"><i class="fa-solid fa-bars"></i></button>
                <button class="resposive-icon px-3 py-2 text-black bg-secondry-1 hidden text-2xl" @click="toggleMenuBar" v-if="menubarOpen"><i class="fa-solid fa-x"></i></button>
                    <ul class="flex flex-wrap items-center ul-menu h-full" v-if="menubarOpen || windowWidth >= 1023.999999999999999">
                        <li class="list-item">
                            <span class="span-dec relative w-full" :class="{ active: isRouteActive('/') }"><i class="fa-solid fa-house me-2"></i>الرئيسية</span>
                        </li>
                        <li class="list-item" @click="toggleSubMenu('1')">
                            <span class="span-dec relative"><i class="fa-solid fa-globe me-2"></i>رحلات سياحية<i class="fa-solid fa-caret-down text-primary ms-1" :class="iconRotate1"></i></span>
                            <ul class="sub-menu md:mt-0 mt-5" v-if="subMenu1">
                            <li :class="{ active: isRouteActive('/honordoctor') }" @click="toggleMenuBar"> <i class="fa-solid fa-map me-3"></i>رحلات سياحية لجورجيا</li>
                            <li :class="{ active: isRouteActive('/ProfessionalDoctorate') }" @click="toggleMenuBar"><i class="fa-solid fa-map me-3"></i>رحلات سياحية لأذربيجان</li>
                            </ul>
                        </li>
                        <li class="list-item" @click="toggleSubMenu('2')">
                            <span class="span-dec relative"><i class="fa-solid fa-info me-2"></i>عن الشركة<i class="fa-solid fa-caret-down text-primary ms-1" :class="iconRotate2"></i></span>
                            <ul class="sub-menu md:mt-0 mt-5" v-if="subMenu2">
                            <li :class="{ active: isRouteActive('/honordoctor') }" @click="toggleMenuBar"> <i class="fa-solid fa-circle-info me-3"></i> من نحن</li>
                            <li :class="{ active: isRouteActive('/ProfessionalDoctorate') }" @click="toggleMenuBar"><i class="fa-solid fa-phone me-3"></i> تواصل معنا</li>
                            <li :class="{ active: isRouteActive('/ProfessionalDoctorate') }" @click="toggleMenuBar"><i class="fa-solid fa-sheet-plastic me-3"></i> سياسة الشركة</li>
                            </ul>
                        </li>
                        <li class="list-item" @click="toggleSubMenu('3')">
                            <span class="span-dec relative"><i class="fa-solid fa-location-dot me-2"></i>فروعنا<i class="fa-solid fa-caret-down text-primary ms-1" :class="iconRotate3"></i></span>
                            <ul class="sub-menu md:mt-0 mt-5" v-if="subMenu3">
                            <li :class="{ active: isRouteActive('/honordoctor') }" @click="toggleMenuBar"> <i class="fa-solid fa-map me-3"></i> أذربيجان</li>
                            <li :class="{ active: isRouteActive('/ProfessionalDoctorate') }" @click="toggleMenuBar"><i class="fa-solid fa-map me-3"></i>جورجيا</li>
                            <li :class="{ active: isRouteActive('/ProfessionalDoctorate') }" @click="toggleMenuBar"><i class="fa-solid fa-map me-3"></i>السعودية</li>
                            </ul>
                        </li>
                        <li class="list-item">
                            <span class="span-dec relative"><i class="fa-solid fa-plane me-2"></i>الرحلات الجوية</span>
                        </li>
                        <li class="list-item">
                            <span class="span-dec relative"><i class="fa-solid fa-comments me-2"></i>أراء العملاء</span>
                        </li>
                        <li class="list-item">
                            <span class="span-dec relative"><i class="fa-solid fa-dollar-sign me-2"></i>انشئ رحتلك</span>
                        </li>
                    </ul>
                </nav>
                <button class="fa-solid fa-cart-shopping text-2xl text-primary"></button>
                <button class="fa-solid fa-user text-2xl text-primary ms-5" v-if="windowWidth < 1023.999999999999999"></button>
            </div>
        </div> -->
  </header>
</template>
<script setup>
import { ref, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";
import axios from "axios";
import i18n from "../i18n";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
// import 'path-to-your-style/style.css'; // replace with the correct path

// Import required modules
import { Autoplay, Pagination, Navigation } from "swiper/modules";

const modules = ref([Autoplay, Pagination, Navigation]);

const router = useRouter();
const openMenu = ref(false);
const info = ref([]);
const userInfo = ref({});
const route = useRoute();
const openAccountBox = ref(false);
const isRouteActive = (routePath) => {
  return route.fullPath === routePath;
};
const changeLang = async () => {
  if (i18n.global.locale.value === "en") {
    i18n.global.locale.value = "ar";
    document.body.dir = "rtl";
    localStorage.setItem("lang", i18n.global.locale.value);
    try {
      await router.replace({ params: { lang: i18n.global.locale.value } });
      location.reload();
    } catch (error) {
      router.push("/");
    }
  } else {
    i18n.global.locale.value = "en";
    document.body.dir = "ltr";
    localStorage.setItem("lang", i18n.global.locale.value);
    // this is very important code for changing the fuckin value in the URL
    try {
      await router.replace({ params: { lang: i18n.global.locale.value } });
      location.reload();
    } catch (error) {
      router.push("/");
    }
  }
};

// -------
const currentDay = ref(null);
const currentNumOfDay = ref(null);
const currentMonth = ref(null);
const currentYear = ref(null);
// const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
// const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
onMounted(() => {
  const currentDate = new Date();
  const dayOfWeek = currentDate.getDay();
  currentDay.value = dayOfWeek;
  currentNumOfDay.value = currentDate.getDate();
  const month = currentDate.getMonth();
  currentMonth.value = month;
  currentYear.value = currentDate.getFullYear();
});
const temp = ref(0);
onMounted(() => {
  axios
    .get(
      "https://api.openweathermap.org/data/2.5/weather?q=Georgia&appid=dcc4737f9298c257d7f2332af3149f53"
    )
    .then((res) => {
      temp.value = res.data.main.temp - 273.15;
      temp.value = temp.value.toFixed(2);
    })
    .catch((err) => console.log(err));
});
// --------
const logOut = () => {
  localStorage.clear();
  // router.push({
  //     name: "Home",
  //     params: { lang: i18n.global.locale.value }
  // })
  location.reload();
};

onMounted(async () => {
  await axios
    .get("https://seasonreal.seasonsge.com/appv1real/info")
    .then((data) => {
      info.value = data.data[0];
    });
  if (localStorage.getItem("clientLogin")) {
    const login = JSON.parse(localStorage.getItem("clientLogin"));
    if (login.success) {
      axios
        .get("https://seasonreal.seasonsge.com/appv1real/usersview")
        .then((data) => {
          userInfo.value = data.data.filter((el) => el.id == login.id)[0];
        });
    }
  }
});
</script>
<style lang="scss" scoped>
.min-h-60 {
  min-height: 60px;
}
.bg-gray-200 {
  background: #cecdcd;
}
.bg-main-color {
  background: #fd820e;
}
.main-color {
  color: #fd820e;
}
// .menu {
//     display: none;
// }

// .close {
//     display: none;
// }

// header {
//     .container.not-home {
//         border-bottom: 1px solid #e4e4e4;
//         padding-bottom: 20px;
//     }

//     .logo {
//         img {
//             width: 100px !important;
//         }
//     }

//     .links {
//         li {
//             a {
//                 position: relative;
//                 transition: 0.2s;

//                 &::before {
//                     content: "";
//                     position: absolute;
//                     transition: 0.2s;
//                     width: 0;
//                     height: 3px;
//                     background-color: var(--blue-color);
//                     bottom: -5px;
//                     left: 50%;
//                     transform: translateX(-50%);
//                     border-radius: 50px;
//                 }

//                 &:hover {
//                     color: var(--blue-color) !important;
//                 }

//                 &:hover::before {
//                     width: 100%;
//                 }

//                 &.router-link-active {
//                     color: var(--blue-color) !important;

//                     &::before {
//                         width: 100%;
//                     }
//                 }
//             }
//         }

.lang {
  cursor: pointer;
  transition: 0.2s;

  &:hover {
    color: var(--blue-color);
  }
}
//     }

//     .account {
//         .box {
//             position: absolute;
//             top: 120%;
//             right: 0;
//             box-shadow: 0 0 15px rgba(0, 0, 0, 0.377);
//         }
//     }

//     @media (max-width: 991px) {
//         .container {
//             padding-bottom: 0 !important;
//             border: none !important;
//         }

//         .menu {
//             display: block;
//             cursor: pointer;

//             &.open {
//                 display: none;
//             }
//         }

//         .close {
//             cursor: pointer;

//             &.open {
//                 display: block;
//             }
//         }

//         .links {
//             box-shadow: 0 0 15px rgba(0, 0, 0, 0.158);
//             position: absolute;
//             flex-direction: column;
//             background-color: white;
//             border-radius: 5px;
//             top: -580%;
//             width: 90%;
//             padding: 20px;
//             z-index: 55555;
//             gap: 30px !important;
//             transition: 0.2s;
//             left: 50%;
//             transform: translateX(-50%);
//             width: 90% !important;

//             &.open {
//                 top: 100%;
//             }
//         }
//     }
// }
</style>
