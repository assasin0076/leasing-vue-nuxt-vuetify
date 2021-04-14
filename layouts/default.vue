<template>
  <v-app>
    <my-nav />
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
  export default {
  }
</script>

<style lang="scss">
  @media(min-width: 500px) {
    .header-text {
      font-family: Nekst;
      font-style: normal;
      font-weight: 900;
      font-size: 22px;
    }
  }
  
  .header-text {
    font-family: Nekst;
    font-style: normal;
    font-weight: 900;
    font-size: 54px;
  }
  @media( max-width: 320px ) {
    .container {
      padding: 0px 20px !important;
    }
  }
  @media( min-width: 320px ) and ( max-width: 768px ) {
    .container {
      padding: 0px 36px !important;
    }
  }
  @media ( min-width: 768px ) {
    .container {
      padding: 0px 64px !important;
    }
  }
  
  h2 {
    font-family: poppins;
    font-weight: 400;
  }
</style>