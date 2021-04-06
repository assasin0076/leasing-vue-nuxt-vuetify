<template>
  <v-app>
    <my-nav :width="width"/>
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
        width: 0,
    }),
    methods: {
        updateWidth() {
            this.width = window.innerWidth;
        },
        showWidth() {
            console.log(this.width);
        }
    },
    mounted() {
        this.updateWidth();
        window.addEventListener('resize', this.updateWidth);
    }
  }
</script>

<style lang="scss">
 h2 {
   font-family: poppins;
   font-weight: 400;
 }
</style>