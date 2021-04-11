<template>
    <v-container
    class="mb-16"
      fluid
    >
        <v-carousel
            class="custom-carousel"
            cycle
            
            height="400"
            hide-delimiter-background
            show-arrows-on-hover
        >
            <v-carousel-item
            v-for="(slide, i) in slides"
            :key="i"
            >
            <v-sheet
                :color="colors[i]"
                height="110%"
            >
                <img src='/img/slide1.png' alt="">
                <v-row
                class="fill-height"
                align="center"
                justify="center"
                >
                <div class="display-3 slider-text">
                    {{ slide.text }}
                </div>
                </v-row>
            </v-sheet>
            </v-carousel-item>
        </v-carousel>
    </v-container>
</template>

<script>
  export default {
    data () {
      return {
        colors: [
          'indigo',
        ],
        slides: [
          { text: 'text lalala', img: '~/static/img/slide1.png' }
        ],
      }
    },
  }
</script>

<style lang="scss" scoped>
  .custom-carousel {
    img {
      width: 100%;
      height: 100%;
      object-fit:cover;
    }
    border-radius: 0px 0px 32px 32px;
  }
</style>