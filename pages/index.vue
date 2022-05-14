<template>
  <div class="flex h-screen bg-slate-600 h-[100vh] align-middle text-white text-center">
    <div class="m-auto">
      <div id="title-card" class="m-10">
        <h1 class="text-5xl">World Clock</h1>
        <p class="mt-5 text-xl">International dates and times</p>
      </div>
      <div id="malaysia" class="text-left m-5">
        <h5 class="text-xl my-5 uppercase"> Current location </h5>
        <div id="ip">address</div>
        <div id="address">address</div>
        <hr/>
        Full response:
        <pre id="details">details</pre>
        <p>Your current location is {{ userLocation }}. </p>
        <p> Your IP address is {{ ipAddress }}. </p>
        <p>Current date and time is {{ date }}.</p>
      </div>
      <div id="timer">
        <div class="grid grid-cols-2 gap-5 m-5 text-white">
          <button class="bg-black px-5 py-3">Start timer</button>
          <button class="bg-black px-5 py-3">Reset timer</button>
        </div>
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
      userLocation: '',
    }
  },
  mounted () {
    $.get('http://ipinfo.io', function (response) {
      $('#ip').html('IP: ' + response.ip);
      $('#address').html('Location: ' + response.city + ', ' + response.region);
      $('#details').html(JSON.stringify(response, null, 4));
    }, 'jsonp');
  }
}
</script>
