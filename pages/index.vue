<template>
  <div class="flex h-screen bg-slate-600 h-[100vh] align-middle text-white text-center">
    <div class="m-auto">
      <h1 class="text-5xl">World Clock</h1>
      <p class="mt-5 text-xl">international dates and times</p>
      <div id="malaysia">
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
export default {
  data () {
    return {
      date: new Date(),
    }
  }
}
</script>
