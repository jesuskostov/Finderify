<template>
  <div class="h-100">
    <div class="presentation d-flex align-items-center justify-content-center" :class="{'remove': intro}">
      <div class="container text-left" :class="{'d-none': introContainer}">
        <h2 class="mb-3">Здравей, Здравей!</h2>
        <h4 class="mb-4">Това е <span class="colored">Finderify</span></h4>
        <p><span class="colored">Finderify</span> е уеб приложение създадено с много търпение и старание за да те улесни в намирането на всичко, което пожелаеш. Ако си в град, в който не си бил до сега <span class="colored">Finderify</span> ще бъде твоят герой.</p>
        <p>Ще бъде нужно твоето разрешение, да използваме локацията ти, ако не си съгласен, приложението няма да бъде ефикасно за теб.</p>
        <button @click="present" class="btn">Продължи</button>
      </div>
      <h2 v-if="introContainer" class="logo colored">Finderify</h2>
    </div>
    <!-- Seachbox -->
    <div class="search-container" :class="{ show: show }">
      <div class="container px-0 d-flex flex-column align-items-center">
        <div class="w-100 city-container flex-grow-1">
          <div
            v-for="(city, i) in cities"
            :key="i"
            class="option"
            :class="{ active: city.city == selected }"
            @click="
              locator(city.city, city.lat, city.lng, (selected = city.city))
            "
          >
            <p>{{ city.city }}</p>
          </div>
        </div>
        <button @click="show = false, animate = false" class="btn">Продължи</button>
      </div>
    </div>
    <button @click="showNav" class="cityBtn" :class="{animate: animate}">
      <span class="d-block d-md-none">
        <svg viewBox="0 -30 476.703 476" xmlns="http://www.w3.org/2000/svg">
          <path d="m390.601562 247.710938h32.859376c-17.847657 95.355468-108.097657 153.839843-185.476563 153.839843-55.808594 0-115-30.011719-150.789063-76.457031-2.375-3.019531-6.738281-3.5625-9.777343-1.21875-3.042969 2.34375-3.628907 6.699219-1.3125 9.765625 19.839843 25.507813 45.199219 46.191406 74.179687 60.488281 28.277344 14.015625 58.601563 21.421875 87.699219 21.421875 44.484375 0 91.300781-17.363281 128.453125-47.636719 38.082031-31.035156 63.113281-73.410156 71.253906-120.203124h39.011719l-43.050781-62.390626zm0 0"/><path d="m53.242188 168.195312c17.847656-95.359374 108.097656-153.84375 185.476562-153.84375 55.808594 0 115 30.011719 150.792969 76.457032 2.371093 3.019531 6.734375 3.566406 9.777343 1.21875 3.039063-2.34375 3.625-6.699219 1.308594-9.765625-19.835937-25.507813-45.199218-46.191407-74.179687-60.488281-28.277344-14.015626-58.601563-21.421876-87.699219-21.421876-44.484375 0-91.300781 17.363282-128.453125 47.640626-38.078125 31.035156-63.109375 73.40625-71.25 120.199218h-39.015625l43.050781 62.394532 43.054688-62.390626zm0 0"/><path d="m218.078125 293.070312h37.515625v46.179688h-37.515625zm0 0"/><path d="m189.898438 76.652344h96.90625v12.257812h-96.90625zm0 0"/><path d="m317.351562 339.25v-236.339844h-158v236.339844h44.726563v-53.179688c0-3.867187 3.136719-7 7-7h51.515625c3.867188 0 7 3.132813 7 7v53.179688zm-119.941406-80.308594h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-40h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-40h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-39.171875h-18.117187c-3.863281 0-7-3.136719-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863281-3.132812 7-7 7zm50 119.171875h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-40h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-40h-18.117187c-3.863281 0-7-3.136718-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7zm0-39.171875h-18.117187c-3.863281 0-7-3.136719-7-7 0-3.867187 3.136719-7 7-7h18.117187c3.867188 0 7 3.132813 7 7 0 3.863281-3.132812 7-7 7zm31.882813-14h18.117187c3.867188 0 7 3.132813 7 7 0 3.863281-3.132812 7-7 7h-18.117187c-3.867188 0-7-3.136719-7-7 0-3.867187 3.132812-7 7-7zm0 39.171875h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7h-18.117187c-3.867188 0-7-3.136718-7-7 0-3.867187 3.132812-7 7-7zm0 40h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7h-18.117187c-3.867188 0-7-3.136718-7-7 0-3.867187 3.132812-7 7-7zm0 40h18.117187c3.867188 0 7 3.132813 7 7 0 3.863282-3.132812 7-7 7h-18.117187c-3.867188 0-7-3.136718-7-7 0-3.867187 3.132812-7 7-7zm0 0"/>
      </svg>
      </span>
      <span class="d-none d-md-block">Избери град</span></button>
    <button v-if="showTransport" @click="backBtnFunction" class="cityBtn category">
      <span class="d-block d-md-none">
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 459 459" style="enable-background:new 0 0 459 459;" xml:space="preserve">
          <g>
            <path d="M178.5,140.25v-102L0,216.75l178.5,178.5V290.7c127.5,0,216.75,40.8,280.5,130.05C433.5,293.25,357,165.75,178.5,140.25z"/>
          </g>
        </svg>
      </span>
      <span class="d-none d-md-block">Избери категория</span>
    </button>
    <!-- Intro -->
    <div class="intro"></div>
    <h2 class="intro-title-city text-uppercase"><img v-if="!cityName" class="loading-gif" src="../assets/loading.gif" alt="">{{ cityName }}</h2>

    <!-- Container results -->
    <div
      class="container custom-padding d-flex flex-column align-items-center justify-content-center w-100 mobile-padding"
    >
      <div class="row w-100">
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div
            class="box mobile"
            @click="
              (categoryShow = false), (showTransport = true), (info = transport)
            "
          >
            <img src="../assets/transport.jpg" alt="" />
            <div class="title">
              <h3>Транспорт</h3>
            </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div
            class="box mobile"
            @click="
              (categoryShow = false), (showTransport = true), (info = service)
            "
          >
            <img src="../assets/services.jpg" alt="" />
            <div class="title">
              <h3>Услуги</h3>
            </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div
            class="box mobile"
            @click="
              (categoryShow = false),
                (showTransport = true),
                (info = entertainment)
            "
          >
            <img src="../assets/еntertainments.jpg" alt="" />
            <div class="title">
              <h3>Развлечение</h3>
            </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div
            class="box mobile"
            @click="
              (categoryShow = false), (showTransport = true), (info = care)
            "
          >
            <img src="../assets/care.jpg" alt="" />
            <div class="title">
              <h3>Грижа</h3>
            </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div class="box mobile">
            <img src="../assets/store.jpg" alt="" />
            <div class="title">
              <h3>Магазини</h3>
            </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4 mobile-padding">
          <div class="box mobile">
            <img src="../assets/others.jpg" alt="" />
            <div class="title">
              <h3>Други</h3>
            </div>
          </div>
        </div>
        <transition name="slide-fade">
          <transport v-if="showTransport" @getSelected="category" :info="info" :places="places" />
        </transition>
      </div>
      <!-- Results -->
      <div v-if="showTransport" class="row">
        <div
          v-for="(object, i) in places"
          :key="i"
          class="col-12 col-md-4"
          :class="{ 'd-none': !object.photos }"
        >
          <div
            v-for="(img, i) in object.photos"
            :key="i"
            class="box"
            @click="openMap(object)"
          >
            <div class="working" :class="{ open: object.opening_hours }">
              <span v-if="object.opening_hours">Open</span
              ><span v-else>Close</span>
            </div>
            <img
              :src="
                `https://maps.googleapis.com/maps/api/place/photo?maxwidth=1000&photoreference=${img.photo_reference}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`
              "
              alt=""
            />
            <div class="title">
              <h3>{{ object.name }}</h3>
            </div>
            <div v-if="object.rating" class="rating">
              <p>{{ object.rating }}</p>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 19.481 19.481"
                xmlns:xlink="http://www.w3.org/1999/xlink"
                enable-background="new 0 0 19.481 19.481"
              >
                <g>
                  <path
                    d="m10.201,.758l2.478,5.865 6.344,.545c0.44,0.038 0.619,0.587 0.285,0.876l-4.812,4.169 1.442,6.202c0.1,0.431-0.367,0.77-0.745,0.541l-5.452-3.288-5.452,3.288c-0.379,0.228-0.845-0.111-0.745-0.541l1.442-6.202-4.813-4.17c-0.334-0.289-0.156-0.838 0.285-0.876l6.344-.545 2.478-5.864c0.172-0.408 0.749-0.408 0.921,0z"
                  />
                </g>
              </svg>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.loading-gif {
  width: 50%;
}
/* Enter and leave animations can use different */
/* durations and timing functions.              */
.slide-fade-enter-active {
  transition: all .8s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
.presentation {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  background-color: #fff;
  z-index: 2000;

  &.remove {
    opacity: 0;
    visibility: hidden;
    transition: 0.8s;
    pointer-events: none;
    z-index: -1321;
  }

}
.logo {
  font-size: 50px;
  transform: scale(0);
  animation: logo 1.8s forwards;
  animation-delay: .9s;
}

@keyframes logo {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1.4);
  }
}

.colored {
  color: #9327b4;
}
.cityBtn {
  position: fixed;
  bottom: 80px;
  right: 20px;
  height: 50px;
  z-index: 1040;
  border: 0;
  width: 180px;
  border-radius: 0;
  margin-top: 50px;
  color: #fff;
  font-weight: 600;
  background: #9d50bb; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #6e48aa,
    #9d50bb
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #6e48aa,
    #9d50bb
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  &.category {
    bottom: 20px;
  }

  svg {
    width: 38px;
    height: 38px;
    fill: #fff;
  }

  &.animate {
    svg {
      transform: rotate(360deg);
      transition: 0.6s;
    }
  }
}
.intro {
  height: 300px;
  border-bottom: 6px solid rgba(147, 39, 180, 1);
  background-image: url("../assets/city.png");
  background-size: contain;
}

.intro-title-city {
  margin-top: 20px;
  font-weight: bold;
  font-size: 82px;
  color: rgba(147, 39, 180, 1);
}

.btn {
  width: 60%;
  height: 50px;
  border: 0;
  border-radius: 0;
  margin-top: 50px;
  color: #fff;
  font-weight: 600;
  background: #9d50bb; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #6e48aa,
    #9d50bb
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #6e48aa,
    #9d50bb
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  &:hover {
    color: #fff;
  }
}
.city-container {
  position: relative;
  padding: 20px 0;
  max-height: 80%;
  overflow-y: scroll;

  &::-webkit-scrollbar {
    width: 0.5em;
  }

  &::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  }

  &::-webkit-scrollbar-thumb {
    background-color: rgba(147, 39, 180, 1);
    outline: 1px solid rgba(147, 39, 180, 1);
  }

  .option {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 40px;
    cursor: pointer;

    p {
      margin: 0;
    }

    &:hover {
      background-color: rgba(147, 39, 180, 0.2);
    }

    &.active {
      background-color: rgba(147, 39, 180, 0.3);
    }
  }
}
.custom-mt {
  padding-top: 5%;
}
.category-box {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-bottom: 30px;
  background-color: #fff;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.08), 0 2px 2px rgba(0, 0, 0, 0.12),
    0 4px 4px rgba(0, 0, 0, 0.16), 0 8px 8px rgba(0, 0, 0, 0.2);
  height: 100px;
  border-radius: 4px;

  &.disable {
    opacity: 0.5;
    pointer-events: none;
  }

  svg {
    flex-grow: 1;
    width: 50px;
    height: 50px;
  }

  h5 {
    color: #000;
    font-size: 14px;
    margin: -10px 0 10px 0;
  }

  &:hover {
    svg {
      animation: rotate 1s infinite;
    }
  }
}

.txt {
  text-align: left;
  font-size: 16px;
}

@keyframes rotate {
  0% {
    transform: rotate(10deg);
  }
  50% {
    transform: rotate(-5deg);
  }
  100% {
    transform: rotate(10deg);
  }
}

select {
  height: 40px;
  background-color: #fff;
  margin-bottom: 20px;
}
.choose-city {
  width: 60%;
  height: 50px;
  border: 0;
  border-radius: 4px;
  background-color: #0986de;
  color: #fff;
  margin-top: -5px;

  &.absolute {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 1030;
    border-radius: 0;
  }
}
.city-img {
  width: 50%;
  margin-top: 5%;
}
.findBtn {
  width: 100%;
  border: 0;
  border-radius: 2px;
  height: 48px;
  background-color: #fff;

  &.absolute {
    position: fixed;
    bottom: 20px;
  }
}
.custom-padding {
  padding-top: 5%;
  margin-bottom: 200px;
}
.city-name {
  position: fixed;
  display: flex;
  top: 0;
  left: 0;
  right: 0;
  height: 50px;
  background-color: #0986de;
  z-index: 10;

  h1 {
    margin: 0;
    color: #fff;
    font-size: 20px;
  }
}
.showSearch {
  height: 50px;
  border: 0;
  border-radius: 99999px;
  background-color: #0986de;
  color: #fff;

  &.absolute {
    position: absolute;
    right: 0;
  }
}

.search-container {
  position: fixed;
  top: 0;
  right: 0;
  width: 26%;
  bottom: 0;
  box-shadow: -5px 0px 12px 0px rgba(0, 0, 0, 0.25);
  background-color: #fff;
  transition: 0.6s;
  z-index: 1050;
  color: #000;
  display: flex;
  transform: translate(100%, 0);

  &.show {
    transform: translate(0, 0);
    transition: 0.6s;
  }

  &.hide {
    opacity: 0;
    visibility: hidden;
    transition: 0.6s;
  }
}
.box {
  cursor: pointer;
  position: relative;
  overflow: hidden;
  height: 250px;
  border-radius: 15px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.08), 0 2px 2px rgba(0, 0, 0, 0.12),
    0 4px 4px rgba(0, 0, 0, 0.16), 0 8px 8px rgba(0, 0, 0, 0.2);
  margin-bottom: 30px;

  .working {
    position: absolute;
    width: 60px;
    height: 20px;
    color: #fff;
    top: 10px;
    left: 15px;
    font-size: 12px;
    border-radius: 5px;
    background-color: #b51919;

    &.open {
      background-color: green;
    }
  }

  .rating {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 40px;
    background-color: #b51919;
    z-index: 5;
    transform: rotate(45deg) translate(30%, -50%);
    border: 1px solid gold;

    p {
      margin: 0;
      color: #fff;
    }

    svg {
      width: 15px;
      height: 15px;
      fill: gold;
      margin-left: 8px;
      position: relative;
      top: -2px;
    }
  }

  .title {
    position: absolute;
    text-align: left;
    bottom: 0;
    z-index: 2;
    padding: 0 15px 30px 15px;

    h3 {
      margin: 0;
      color: #fff;
      font-size: 18px;
    }
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgb(4, 4, 4);
    background: linear-gradient(
      0deg,
      rgba(4, 4, 4, 1) 0%,
      rgba(4, 4, 4, 0) 100%
    );
    pointer-events: none;
    transition: 0.6s;
  }

  &:hover {
    &::after {
      background: linear-gradient(
        0deg,
        rgba(4, 4, 4, 1) 0%,
        rgba(4, 4, 4, 0) 100%
      );
      transition: 0.6s;
    }
  }
}
@media (max-width: 768px) {
  .custom-mt {
    margin: 0;
  }
  .custom-padding {
    margin: 60px 0px 0 0;
  }
  .city-img {
    width: 100%;
  }
  .txt {
    font-size: 13px;
  }
  .choose-city {
    width: 100%;
  }
  .search-container {
    top: 0;
    width: 100%;
    height: 100%;
    transform: translate(110%, 0);
    bottom: 0;
    padding: 0;
    border-radius: 0;
    left: 0;
    right: 0;

    &.show {
      transform: translate(0, 0);
    }
  }
  .intro {
    height: 0;
  }
  .intro-title-city {
    position: fixed;
    display: flex;
    align-items: center;
    justify-content: center;
    top: 0;
    z-index: 123;
    left: 0;
    right: 0;
    background: #fff;
    margin: 0;
    padding: 10px 0;
    font-size: 28px;
    box-shadow: 0px 1px 16px 0px rgba(0,0,0,0.75);
    height: 65px;
    white-space: nowrap;
    overflow-x: scroll;
  }
  .box {
    border-radius: 0;
    margin-bottom: 0;

    &.mobile {
      margin-bottom: 0;
      border-radius: 0;
    }
  }
  .mobile-padding {
    padding: 0;
  }
  .cityBtn {
    right: 0;
    bottom: 50px;
    width: 20%;
    background: #9327b4;
    border-bottom-left-radius: 30px;
    background: rgba(147, 39, 180, 1);

    &.category {
      left: 0;
      bottom: 50px;
      border-bottom-left-radius: 0;
      border-bottom-right-radius: 30px;
      background: rgba(147, 39, 180, 1);
    }
  }
  
}
</style>

<script>
import axios from "axios";
import city from "../bg";
import transport from "../components/transport";

export default {
  components: {
    transport,
  },
  data() {
    return {
      intro: false,
      introContainer: false,
      animate: false,
      loaded: false,
      info: "",
      categoryShow: true,
      showTransport: false,
      hideAll: false,
      selected: undefined,
      currentCity: "",
      showBox: false,
      transport: "transport",
      service: "service",
      entertainment: "entertainment",
      care: "care",
      store: "store",
      other: "other",
      disable: true,
      showFindBtn: false,
      backBtn: false,
      getType: "",
      typeName: "",
      show: false,
      hide: false,
      type: "",
      radius: "10",
      lat: 0,
      lng: 0,
      places: null,
      cities: [],
      choosenCity: "",
      cityName: "",
      distance: [],
      // stores: ['clothing_store', 'shoe_store', 'store', 'supermarket', 'book_store', 'bicycle_store', 'pet_store'],
      // others: ['fire_station', 'hospital', 'police', 'church', 'museum', 'school', 'stadium', 'tourist_attraction', 'zoo', 'art_gallery', 'library']
    };
  },
  created() {
    // GET CURRENT CITY

    let boxHeight = (window.innerHeight - 64) / 6
    setTimeout(() => {
      let boxes = document.getElementsByClassName('mobile')
      for (let item of boxes) {
        item.style.height = boxHeight + 'px'
      }
    }, 10)


    this.cities = city;
    navigator.geolocation.getCurrentPosition(
      (position) => {
        this.lat = position.coords.latitude.toFixed(6);
        this.lng = position.coords.longitude.toFixed(6);
        axios
          .get(
            `https://maps.googleapis.com/maps/api/geocode/json?latlng=${this.lat},${this.lng}&sensor=true&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`
          )
          .then((res) => {
            let geometryLng = res.data.results[0].geometry.location.lat + "";
            let geometryLat = res.data.results[0].geometry.location.lng + "";
            let readyGeometry =
              geometryLng.substring(0, 4) + "," + geometryLat.substring(0, 4);
            this.choosenCity =
              readyGeometry +
              "," +
              res.data.results[0].address_components[2].long_name;
            let onlyCityName = this.choosenCity.split(",");
            this.cityName = onlyCityName[2];
            this.selected = onlyCityName[2];
          });
      },
      (error) => {
        console.log(error);
      }
    );
  },
  computed: {
    cordinates() {
      return `${this.lat}, ${this.lng}`;
    },
  },
  methods: {
    category(value) {
      this.type = value;

      // Get results
      setTimeout(() => {
        const URL = `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=${
          this.lat
        },${this.lng}&type=${this.type}&radius=${this.radius *
          1000}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`;
        axios
          .get(URL)
          .then((res) => {
            this.places = res.data.results;
          })
          .catch((err) => {
            console.log(err.message);
          });
        this.show = false;
        this.hide = true;
      }, 100);

      // Distance calculate
      setTimeout(() => {
        this.places.map((id) => {
          axios
            .get(
              `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/distancematrix/json?units=metric&origins=${this.lat},${this.lng}&destinations=place_id:${id.place_id}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`
            )
            .then((res) => {
              console.log(res.data.rows[0].elements[0].distance.text);
            });
        });
      }, 4000);
    },
    locator(city, lat, lng) {
      let roundLat = lat.substring(0, 4);
      let roundLng = lng.substring(0, 4);
      this.choosenCity = roundLat + "," + roundLng + "," + city;
      let splitCordinates = this.choosenCity.split(",");
      this.lat = splitCordinates[0];
      this.lng = splitCordinates[1];
      this.cityName = splitCordinates[2];
      this.showBox = true;
      this.disable = false;
    },
    showNav() {
      this.animate = true
      setTimeout(() => {
        this.show = true
      }, 800)
    },
    openMap(object) {
      window.open(
        `https://www.google.com/maps/place/?q=place_id:${object.place_id}`,
        "_blank"
      );
    },
    present() {
      this.introContainer = true
      setTimeout(() => {
        this.intro = true
      }, 3100)
    },
    backBtnFunction() {
      this.showTransport = false
      this.categoryShow = true 
      this.places = null

      let boxHeight = (window.innerHeight - 64) / 6
      setTimeout(() => {
        let boxes = document.getElementsByClassName('mobile')
        for (let item of boxes) {
          item.style.height = boxHeight + 'px'
        }
      }, 10)

    }
  },
  mounted() {
    console.log('pak');
  }
};
</script>
