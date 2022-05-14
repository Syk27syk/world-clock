<template>
  <div class="flex h-screen bg-slate-600 h-[100vh] align-middle text-white text-center">
    <div class="m-auto">
      <div id="title-card" class="m-10">
        <h1 class="text-5xl">World Clock</h1>
        <p class="mt-5 text-xl">International dates and times</p>
      </div>
      <div id="malaysia" class="text-left m-5">
        <p id="address">Your current location is {{ userLocation }}. </p>
        <p id="ip"> Your IP address is {{ userIP }}. </p>
        <pre id="details">Details: {{ details }}</pre>
        <p class="my-5">Current date and time is {{ date }}.</p>
        <div class="countdown">
          <h5>Count down until new year 2023:</h5>
          <div class="flex flex-row">
            <p id="days"> days </p>
            <p id="hours"> hours </p>
            <p id="mins"> mins </p>
            <p id="secs"> secs </p>
            <p id="end"> end </p>
          </div>
        </div>
      </div>
      <div id="timer">
        <div class="grid grid-cols-2 gap-5 m-5 text-white">
          <button class="bg-black px-5 py-3">Start timer</button>
          <button class="bg-black px-5 py-3">Reset timer</button>
        </div>
      </div>
      <div id="page-event-log">
        <p>Page event log: </p>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
export default {
  data () {
    return {
      date: new Date(),
    }
  },
  mounted () {
    $.get('http://ipinfo.io', function (response) {
      $('#ip').html('IP: ' + response.ip);
      $('#address').html('Location: ' + response.city + ', ' + response.region);
      $('#details').html(JSON.stringify(response, null, 4));
    }, 'jsonp');
  },
  methods: {
    increment () {
      this.userIP = this.userIP++;
    },
    userIP () {
      $.get('http://ipinfo.io', function (response) {
        const userIP = $(response.ip);
        return userIP
      }, 'jsonp');
    },
    userAddress () {
      $.get('http://ipinfo.io', function (response) {
        const userAddress = $(response.city + ', ' + response.region);
        return userAddress
      }, 'jsonp');
    },
    details () {
      $.get('http://ipinfo.io', function (response) {
        const details = $('#details').html(JSON.stringify(response, null, 4));
        return details
      }, 'jsonp');
    },
    gelocation () {
      navigator.geolocation.getCurrentPosition(function(position) {
        const latitude = position.coords.latitude;
        const longitude = position.coords.longitude;
        return [latitude, longitude];
      });
    },
    countDown() {
      const countDownDate = new Date().getTime();
      const myfunc = setInterval(function() {
        const now = new Date().getTime();
        const timeleft = countDownDate - now;
        const days = Math.floor(timeleft / (1000 * 60 * 60 * 24));
        const hours = Math.floor((timeleft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutes = Math.floor((timeleft % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((timeleft % (1000 * 60)) / 1000);
        document.getElementById('days').innerHTML = days + 'd'
        document.getElementById('hours').innerHTML = hours + 'h'
        document.getElementById('mins').innerHTML = minutes + 'm'
        document.getElementById('secs').innerHTML = seconds + 's'
        if (timeleft < 0) {
          clearInterval(myfunc);
          document.getElementById('days').innerHTML = ''
          document.getElementById('mins').innerHTML = ''
          document.getElementById('secs').innerHTML = ''
          document.getElementById('end').innerHTML = 'HAPPY NEW YEAR!';
        }
      }, 1000)
    }
  }
}
</script>
