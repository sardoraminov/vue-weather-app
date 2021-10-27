<template>
  <div class="home wh-app">
    <div class="titles">
      <h1>Weather App <img src="../assets/weather.png" alt="Weather" /></h1>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iste,
        consequatur
      </p>
    </div>
    <div class="weathers">
      <input
        type="text"
        v-model="query"
        placeholder="Enter your city..."
        autocomplete="off"
      />
      <button @click="fetchWeather" type="button">Go</button>
      <div  v-if="typeof weather.main != 'undefined'" class="weather-wrap">
        <h1 class="city">{{ weather.name }} {{ weather.sys.country }}</h1>
        <h5 class="today">{{dateBuilder()}}</h5>
        <div class="weathers-temp">
          <h1 class="temp">{{ Math.round(weather.main.feels_like) }}°C</h1>
          <p class="status">{{ weather.weather[0].main }}</p>
        </div>
      </div>``

      <div  v-else class="weather-wrap">
        <h1>Please, enter valid city</h1>
      </div>

      <footer>
        Developed by<a href="https://instagram.com/s_aminoff">SARDOR</a>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",

  data() {
    return {
      base_url: `https://api.openweathermap.org/data/2.5/`,
      api_key: "ff739f4aecaccaa3e01cd2590f59d60e",
      query: "",
      weather: {},
      errMsg: "",
    };
  },
  methods: {
    fetchWeather(e) {
      fetch(
        `${this.base_url}weather?q=${this.query}&appid=${this.api_key}&units=metric`
      )
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          this.setResults(data);
        });
    },

    setResults(result) {
      this.weather = result;
    },

    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>


<style scoped>
.home {
  margin-top: 40px;
  color: #fff;
}

.titles {
  padding: 0 15px;
}

.weather-wrap {
  margin-top: 10px;
}

.titles h1 {
  font-family: "Montserrat", sans-serif;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  text-shadow: 2px 2px rgba(58, 58, 58, 0.685);
}

.titles h1 img {
  margin-left: 15px;
}

.titles p {
  margin-top: 10px;
  font-family: "Quicksand", sans-serif;
  color: rgba(255, 255, 255, 0.863);
  letter-spacing: 1px;
}

.weathers {
  margin-top: 20px;
}

.weathers input {
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(15px);
  border: none;
  outline: none;
  padding: 10px 15px;
  color: #fff;
  font-family: "Quicksand", sans-serif;
  border: 2px solid rgba(255, 255, 255, 0.226);
  border-radius: 5px;
  transition: all 0.4s ease;
}

.weathers button {
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(15px);
  border: none;
  outline: none;
  padding: 10px 15px;
  color: #fff;
  font-family: "Quicksand", sans-serif;
  border: 2px solid rgba(255, 255, 255, 0.226);
  border-radius: 5px;
  transition: all 0.4s ease;
  cursor: pointer;
}

.weathers button:hover {
  border-color: #fff;
}

.weathers input:focus {
  margin-bottom: 10px;
  border-color: #fff;
}

.weathers input::placeholder {
  color: rgba(255, 255, 255, 0.61);
}

.weathers .city {
  text-shadow: 2px 2px rgba(58, 58, 58, 0.685);

  margin-top: 15px;
}

.weathers .today {
  font-style: italic;
  font-family: "Quicksand", sans-serif;
  font-weight: 400;
  color: rgba(250, 250, 250, 0.623);
}

.weathers .weathers-temp {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}

.weathers-temp h1 {
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(15px);
  padding: 10px;
  font-size: 53px;
  text-shadow: 2px 2px rgba(58, 58, 58, 0.685);
  border-radius: 5px;
}

.weathers-temp p {
  margin-top: 10px;
}

footer {
  margin-top: 100px;
  color: rgba(250, 250, 250, 0.623);
  font-family: "Quicksand", sans-serif;
}

footer a {
  text-decoration: none;
  color: rgba(250, 250, 250, 0.623);
  margin-left: 5px;
}
</style>