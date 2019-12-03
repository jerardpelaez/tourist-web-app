<template>
  <div class="home">
    <v-container>
      <h1 class="text-center font-weight-light header">
        Explore the Wonders of
        <span class="japan">Japan</span>
      </h1>
      <v-layout row>
        <v-flex xs6 md4 v-for="info in infos" :key="info.title" class="mt-10">
          <v-card class="ma-3" max-width="400" hover ripple @click="modal(info)">
            <v-img class="white--text align-end" height="200px" :src="info.src"></v-img>
            <v-card-text class="text--primary">
              <div class="title font-weight-light card-info">{{info.location}}, {{info.title}}</div>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
    <v-row justify="center">
      <v-dialog v-model="dialog" max-width="1000px">
        <v-card>
          <v-img :src="city.img" height="300px" dark></v-img>
          <h1 class="text-center mt-5 display-2">
            <span class="card-head red--text text--lighten-3">{{city.name}}</span>
          </h1>

          <v-list class="ma-10">
            <h3 class="ml-7 headline helpers font-weight-medium">Weather Information</h3>
            <v-divider></v-divider>
            <v-list-item>
              <v-img
                :src="`http://openweathermap.org/img/wn/${city.weather.icon}@2x.png`"
                class="image"
              />
              <v-list-item-content>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'broken clouds'"
                  class="title"
                >Cloudy</v-list-item-subtitle>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'scattered clouds'"
                  class="title"
                >Cloudy</v-list-item-subtitle>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'clear sky'"
                  class="title"
                >Sunny</v-list-item-subtitle>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'few clouds'"
                  class="title"
                >Mildy Cloudy</v-list-item-subtitle>
                <v-list-item-subtitle v-if="city.weather.description == 'mist'" class="title">Misty</v-list-item-subtitle>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'shower rain'"
                  class="title"
                >Rainy</v-list-item-subtitle>
                <v-list-item-subtitle v-if="city.weather.description == 'rain'" class="title">Rainy</v-list-item-subtitle>
                <v-list-item-subtitle
                  v-if="city.weather.description == 'thunderstorm'"
                  class="title"
                >Stormy</v-list-item-subtitle>
                <v-list-item-subtitle v-if="city.weather.description == 'snow'" class="title">Snowy</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <h3 class="ml-7 headline helpers font-weight-medium">Nearby Places to Visit</h3>
            <v-divider></v-divider>
            <v-list-item
              v-for="(item, index) in city.details"
              :key="index"
              class="font-weight-bold"
            >
              <v-list-item-content>
                <v-list-item-title class="headline mb-2 font-weight-light">{{ item.name }}</v-list-item-title>
                <v-list-item-subtitle>{{ item.location.address }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
          <v-divider></v-divider>
        </v-card>
      </v-dialog>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "home",
  components: {},
  data() {
    return {
      city: {
        name: "",
        img: "",
        weather: [],
        details: []
      },
      dialog: false,
      infos: [
        {
          src:
            "https://images.unsplash.com/photo-1536098561742-ca998e48cbcc?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=762&q=80",
          location: "Tokyo Tower",
          title: "Tokyo"
        },
        {
          src:
            "https://images.unsplash.com/photo-1571267468911-a8d098c0f900?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80",
          location: "Prefectura de Kanagawa",
          title: "Yokohama"
        },
        {
          src:
            "https://images.unsplash.com/photo-1558862107-d49ef2a04d72?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80",
          location: "Fushimi Inari",
          title: "Kyoto"
        },
        {
          src:
            "https://images.unsplash.com/photo-1564839324965-32af59c0435a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1190&q=80",
          location: "Osaka Tower",
          title: "Osaka"
        },
        {
          src:
            "https://images.unsplash.com/photo-1519105467443-4779d0fb729d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80",
          location: "Sapporo Ice Festival",
          title: "Sapporo"
        },
        {
          src: "https://www.japan-guide.com/g18/3300_11.jpg",
          location: "Nagoya Castle",
          title: "Nagoya"
        }
      ]
    };
  },

  methods: {
    modal(item) {
      this.dialog = true;
      this.city.name = item.title;
      this.city.img = item.src;
      this.getAPI(item.title);
    },
    getAPI(city) {
      const apiKey = "a0beb7aeb3f0c7871f11d37066cac05a";
      const api = `http://api.openweathermap.org/data/2.5/forecast?q=${city}&appid=${apiKey}`;

      const client_id = "TIUCRXEY4V3K42C1X5FXD0VUA0BECILI1SN5HB454XA5S1D0";
      const client_secret = "LX12MHCXH1CVKBYRJSR3AV2D4BYDCE2DWSIDYRKUQFHIUZSX";
      const setDetail = `https://api.foursquare.com/v2/venues/search?near=${city}&client_id=${client_id}&client_secret=${client_secret}&v=20191203`;

      axios.get(api).then(({ data }) => {
        this.city.weather = data.list[0].weather[0];
      });

      axios.get(setDetail).then(({ data }) => {
        this.city.details = data.response.venues.slice(0, 5);
      });
    }
  }
};
</script>

<style>
.header {
  margin-top: 60px;
  font-family: "Gupter", serif;
  font-size: 60px;
}
.helpers {
  font-family: "Dosis", sans-serif;
}
.card-head {
  font-family: "Permanent Marker", cursive;
}
.japan {
  font-family: "Calistoga", cursive;
  font-size: 70px;
}
.image {
  max-width: 100px;
}
.card-info {
  font-family: "Gupter", serif;
}
@media only screen and (max-width: 600px) {
  .header {
    margin-top: 60px;
    font-family: "Gupter", serif;
    font-size: 40px;
  }
  .japan {
    font-family: "Calistoga", cursive;
    font-size: 50px;
  }
}
</style>