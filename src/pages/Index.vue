<template>
  <q-page class="flex flex-center">
    <!-- <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"
    > -->
    <download></download>
  </q-page>
</template>

<script>
import Download from '../components/Download.vue'
export default {
  name: 'PageIndex',
  components: {
    "download": Download
  }
}
</script>
