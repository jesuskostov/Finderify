<template>
  <div class="h-100">
    <!-- Seachbox -->
    <div class="search-container" :class="{'show': show}">
      <div class="container px-0 d-flex flex-column align-items-center">
          <div class="w-100 city-container flex-grow-1">
            <div v-for="(city, i) in cities" :key="i" class="option" :class="{active: city.city == selected}"  @click="locator(city.city, city.lat, city.lng, selected = city.city)">
              <p>{{city.city}}</p>
            </div>
          </div>
        <button @click="show = false" class="btn">Продължи</button>
      </div>
    </div>
    <button @click="showNav" class="cityBtn">Избери град</button>
    <button @click="showTransport = false, categoryShow = true, places = null" class="cityBtn category">Избери категория</button>
    <!-- Intro -->
    <div class="intro"></div>
    <h2 class="intro-title-city text-uppercase">{{cityName}}</h2>

    <!-- Container results -->
    <div class="container custom-padding d-flex flex-column align-items-center justify-content-center w-100">
      <div class="row w-100">
        <div v-if="categoryShow" class="col-md-4">
          <div class="box" @click="categoryShow = false, showTransport = true, info = transport">
              <img src="../assets/transport.jpg" alt="">
              <div class="title">
                <h3>Транспорт</h3>
              </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4">
          <div class="box" @click="categoryShow = false, showTransport = true, info = service">
              <img src="../assets/services.jpg" alt="">
              <div class="title">
                <h3>Услуги</h3>
              </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4">
          <div class="box" @click="categoryShow = false, showTransport = true, info = entertainment">
              <img src="../assets/еntertainments.jpg" alt="">
              <div class="title">
                <h3>Развлечение</h3>
              </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4">
          <div class="box" @click="categoryShow = false, showTransport = true, info = care">
              <img src="../assets/care.jpg" alt="">
              <div class="title">
                <h3>Грижа</h3>
              </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4">
          <div class="box">
              <img src="../assets/store.jpg" alt="">
              <div class="title">
                <h3>Магазини</h3>
              </div>
          </div>
        </div>
        <div v-if="categoryShow" class="col-md-4">
          <div class="box">
              <img src="../assets/others.jpg" alt="">
              <div class="title">
                <h3>Други</h3>
              </div>
          </div>
        </div>

        <transport v-if="showTransport" @getSelected="category" :info="info" />
      </div>
      <!-- Results -->
      <h2 v-for="(km, i) in distance" :key="i">test{{km}}</h2>
      <div v-if="showTransport" class="row">
        <div v-for="(object, i) in places" :key="i" class="col-12 col-md-4" :class="{'d-none': !object.photos}">
          <div v-for="(img, i) in object.photos" :key="i" class="box" @click="test(object)">
            <div class="working" :class="{'open': object.opening_hours}"><span v-if="object.opening_hours">Open</span><span v-else>Close</span></div>
              <img :src="`https://maps.googleapis.com/maps/api/place/photo?maxwidth=1000&photoreference=${img.photo_reference}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`" alt="">
            <div class="title">
              <h3>{{object.name}}</h3>
            </div>
            <div v-if="object.rating" class="rating">
              <p>{{object.rating}}</p>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 19.481 19.481" xmlns:xlink="http://www.w3.org/1999/xlink" enable-background="new 0 0 19.481 19.481">
                <g>
                  <path d="m10.201,.758l2.478,5.865 6.344,.545c0.44,0.038 0.619,0.587 0.285,0.876l-4.812,4.169 1.442,6.202c0.1,0.431-0.367,0.77-0.745,0.541l-5.452-3.288-5.452,3.288c-0.379,0.228-0.845-0.111-0.745-0.541l1.442-6.202-4.813-4.17c-0.334-0.289-0.156-0.838 0.285-0.876l6.344-.545 2.478-5.864c0.172-0.408 0.749-0.408 0.921,0z"/>
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
  background: #9D50BB;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #6E48AA, #9D50BB);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #6E48AA, #9D50BB); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  &.category {
    bottom: 20px;
  }
}
.intro {
  height: 300px;
  border-bottom: 6px solid rgba(147, 39, 180, 1);
  background-image: url('../assets/city.png');
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
  background: #9D50BB;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #6E48AA, #9D50BB);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #6E48AA, #9D50BB); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

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
  box-shadow: 0 1px 1px rgba(0,0,0,0.08), 
                0 2px 2px rgba(0,0,0,0.12), 
                0 4px 4px rgba(0,0,0,0.16), 
                0 8px 8px rgba(0,0,0,0.20);
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
  0%{
    transform: rotate(10deg);
  }
  50%{
    transform: rotate(-5deg)
    }
  100%{
    transform: rotate(10deg);
  }
}

select {
  height: 40px;
  background-color: #fff;
  margin-bottom: 20px;
}
.choose-city{
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
  box-shadow: -5px 0px 12px 0px rgba(0,0,0,0.25);
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
  box-shadow: 0 1px 1px rgba(0,0,0,0.08), 
                0 2px 2px rgba(0,0,0,0.12), 
                0 4px 4px rgba(0,0,0,0.16), 
                0 8px 8px rgba(0,0,0,0.20);
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
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgb(4,4,4);
    background: linear-gradient(0deg, rgba(4,4,4,1) 0%, rgba(4,4,4,0) 100%);
    pointer-events: none;
    transition: 0.6s;
  }

  &:hover {
    &::after {
      background: linear-gradient(0deg, rgba(4,4,4,1) 0%, rgba(4,4,4,0) 100%);
      transition: 0.6s;
    }
  }
  
}
@media (max-width: 768px) {
  .custom-mt {
    margin: 0;
  }
  .custom-padding {
    padding-top: 30%;
    padding-bottom: 20%;
  }
  .city-img {
    width: 100%;
  }
  .txt {
    font-size: 13px;
  }
  .choose-city{
    width: 100%;
  }
  .search-container {
    top: 0;
    width: 100%;
    height: 100%;
    transform: translate(0, 0);
    bottom: 0;
    padding: 0;
    border-radius: 0;
    left: 0;
    right: 0;
  }
}
</style>

<script>
import axios from 'axios';
import city from '../bg'
import transport from '../components/transport'

export default {
  components: {
    transport,
  },
  data() {
    return {
      info: '',
      categoryShow: true,
      showTransport: false,
      hideAll: false,
      selected: undefined,
      currentCity: '',
      showBox: false,
      transport: 'transport',
      service: 'service',
      entertainment: 'entertainment',
      care: 'care',
      store: 'store',
      other: 'other',
      disable: true,
      showFindBtn: false,
      backBtn: false,
      getType: '',
      typeName: '',
      show: false,
      hide: false,
      type: "",
      radius: "10",
      lat: 0,
      lng: 0,
      places: [],
      cities: [],
      choosenCity: '',
      cityName: '',
      distance: [],
      // stores: ['clothing_store', 'shoe_store', 'store', 'supermarket', 'book_store', 'bicycle_store', 'pet_store'],
      // others: ['fire_station', 'hospital', 'police', 'church', 'museum', 'school', 'stadium', 'tourist_attraction', 'zoo', 'art_gallery', 'library']
    }
  },
  created() {
        // GET CURRENT CITY
      this.cities = city;
      navigator.geolocation.getCurrentPosition(position => {
        console.log(123);
        this.lat = position.coords.latitude.toFixed(6)
        this.lng = position.coords.longitude.toFixed(6)
        axios.get(`https://maps.googleapis.com/maps/api/geocode/json?latlng=${this.lat},${this.lng}&sensor=true&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`)
        .then( res => {
          let geometryLng = res.data.results[0].geometry.location.lat + '';
          let geometryLat = res.data.results[0].geometry.location.lng + '';
          let readyGeometry = geometryLng.substring(0, 4) + ',' + geometryLat.substring(0, 4);
          this.choosenCity = readyGeometry + ',' + res.data.results[0].address_components[2].long_name
          let onlyCityName = this.choosenCity.split(",")
          this.cityName = onlyCityName[2]
          this.selected = onlyCityName[2]
        })
      },
      error => {
        console.log(error);
      })
  },
  computed: {
    cordinates() {
      return `${this.lat}, ${this.lng}`
    },
  },
  methods: {
    category(value) {
      this.type = value

      // Get results
      setTimeout(() => {
        const URL = `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=${
          this.lat
        },${this.lng}&type=${this.type}&radius=${this.radius *
          1000}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`;
        axios.get(URL).then(res => {
          this.places = res.data.results
        }).catch(err => {
          console.log(err.message);
        })
        this.show = false
        this.hide = true
      }, 100)

      // Distance calculate
      setTimeout(() => {
        this.places.map( id => {
          const distance = `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/distancematrix/json?units=metric&origins=${this.lat},${this.lng}&destinations=place_id:${id.place_id}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`
          axios.get(distance).then( res => {
            this.distance = res.data.rows[0].elements[0].distance.text
            console.log(this.distance);
          })
        })
      }, 10000)
      

    },
    locator(city, lat, lng) {
      let roundLat = lat.substring(0, 4)
      let roundLng = lng.substring(0, 4)
      this.choosenCity = roundLat + ',' + roundLng + ',' + city
      let splitCordinates = this.choosenCity.split(',')
      this.lat = splitCordinates[0]
      this.lng = splitCordinates[1]
      this.cityName = splitCordinates[2]
      this.showBox = true
      this.disable = false
    },
    showNav() {
      this.show = true
    },
    test(object) {
      window.open(`https://www.google.com/maps/place/?q=place_id:${object.place_id}`, "_blank");    
    },
  }
}
</script>
