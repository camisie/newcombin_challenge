<template>
  <div class="header">
    <v-tabs
        background-color="#009A48"
        color="black"
        grow
        height="72px"
    >
      <v-tabs-slider color="black"></v-tabs-slider>
      <v-tab
          v-for="tab in tabs"
          :key="tab"
      >
        {{ tab }}
      </v-tab>
    </v-tabs>
  </div>

</template>

<script>
export default {
  name: "AppHeader",
  data () {
    return {
      tabs: [
        "Home", "Other Page"
      ],
    }
  },
}
</script>

<style scoped></style>