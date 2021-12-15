<template>
  <div class="btn-group">
    <h2>{{ msg }}</h2>
    <div class="btn-wrapper">
      <button
        v-for="city in cities"
        v-bind:key="city.id"
        @click="onButtonClick(city.name)"
      >
        <img
          src="../assets/icons/berlin-512x512-101649.png"
          alt=""
        />
        {{ city.name }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Cities',
  props: {
    msg: String,
  },
  data() {
    return {
      cities: [
        {
          name: 'Berlin',
          icon_url:
            '../assets/icons/berlin-512x512-101649.png',
        },
        {
          name: 'Braunschweig',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'Elsterberg',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'Hamburg',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'Paris',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'London',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'New York',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'Shanghai',
          icon_url: '../assets/icons/berlin.png',
        },
        {
          name: 'Mexico City',
          icon_url: '../assets/icons/berlin.png',
        },
      ],
    }
  },
  methods: {
    onButtonClick(city) {
      this.$emit('citySelect', { city })
    },
  },

  // watch, which city is selected: and get the icon url of the pokemon
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  margin-bottom: 25px;
}

.btn-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

img {
  height: 40px;
}

button {
  padding: 5px 10px;
  font-weight: 700;
  margin-bottom: 20px;
  margin-right: 20px;
  color: #313131;
  font-size: 20px;
  border: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 10px 0px 10px;
  transition: 0.4s;
}

button:focus {
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 10px 0px 10px 0px;
}

button:last-of-type {
  margin-right: 0;
}

button:hover {
  color: #42b983;
  cursor: pointer;
}
</style>
