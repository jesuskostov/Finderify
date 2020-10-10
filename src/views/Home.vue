<template>
  <div>
    <div class="city-name align-items-center" :class="{'d-none': show}">
      <h1 class="flex-grow-1">{{cityName}}</h1>
    </div>

    <div class="search-container" :class="{'show': show}">
      <div class="container py-4 d-flex flex-column justify-content-between align-items-center h-100">
        <div class="d-flex justify-content-end w-100">
          <button @click="show = false" class="showSearch absolute">Close</button>
        </div>
        <div class="w-100">
          <h2 class="mb-5">Find your place</h2>
          <select class="w-100" v-model="choosenCity" @change="locator">
            <option v-for="(city, i) in cities" :key="i" :value="`${city.lat},${city.lng},${city.city}`">{{city.city}}</option>
          </select>
          <select class="w-100" v-model="choosenCity" @change="locator">
            <option value="none">Choose city</option>
            <option v-for="(city, i) in cities" :key="i" :value="`${city.lat},${city.lng},${city.city}`">{{city.city}}</option>
          </select>
        </div>
        <button @click="getObjects" class="findBtn">Find places</button>
      </div>
    </div>
    
    <div class="container custom-padding">
      <p v-if="!hide" class="txt">Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio vero atque ducimus, adipisci quisquam id provident reiciendis corrupti, vitae ut deleniti tempore delectus voluptatem blanditiis. Debitis eveniet explicabo et quam.</p>
      <img v-if="!hide" class="city-img" src="../city.png" alt="">
      <button @click="show = true" class="choose-city" :class="{'absolute': hide}"><span v-if="cityName == ''">Choose your city</span> <span v-else>{{cityName}}</span></button>
      <div class="row">
        <div v-for="(object, i) in places" :key="i" class="col-12 col-md-4" :class="{'d-none': !object.photos}">
          <div v-for="(img, i) in object.photos" :key="i" class="box">
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
.txt {
  text-align: left;
  font-size: 13px;
}
select {
  height: 40px;
  background-color: #fff;
  margin-bottom: 20px;
}
.choose-city{
  width: 100%;
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
  }
}
.city-img {
  width: 100%;
  margin-top: 15%;
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
  padding-top: 30%;
  padding-bottom: 20%;
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
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #0986de;
  opacity: 0;
  visibility: hidden;
  transition: 0.6s;
  z-index: 1036;
  color: #fff;

  &.show {
    opacity: 1;
    visibility: visible;
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
  }
}
</style>

<script>
import axios from 'axios';
import city from '../bg'

export default {
  data() {
    return {
      show: false,
      hide: false,
      type: "jewelry_store",
      radius: "10",
      lat: 0,
      lng: 0,
      places: [],
      cities: [],
      choosenCity: '',
      cityName: '',
    }
  },
  created() {
    this.cities = city;
      navigator.geolocation.getCurrentPosition(position => {
        this.lat = position.coords.latitude.toFixed(6)
        this.lng = position.coords.longitude.toFixed(6)

        // city.filter( obj => {
        //   let currentLat = obj.lat
        //   let currentLng = obj.lng

        //   if(currentLat == this.lat && currentLng == this.lng) {
        //     console.log(123);
        //   }
        // })
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
    getObjects() {
      const URL = `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=${
        this.lat
      },${this.lng}&type=${this.type}&radius=${this.radius *
        1000}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`;
      axios.get(URL).then(res => {
        this.places = res.data.results
        console.log(this.places);
      }).catch(err => {
        console.log(err.message);
      })
      this.show = false
      this.hide = true
    },
    locator() {
      let splitCordinates = this.choosenCity.split(',')
      this.lat = splitCordinates[0]
      this.lng = splitCordinates[1]
      this.cityName = splitCordinates[2]
    },
  }
}
</script>