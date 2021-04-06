<template>
    <v-container class="calc-cont">
        <v-col>
            <h1 class="mb-10">
                    Рассчитайте стоимость <br> автомобиля в лизинг
            </h1>
            <v-row>
                <v-container>
                    <v-row

                    justify="space-between"
                    >
                        <v-col
                            cols="12"
                            md="4"
                        >
                            <v-form ref="form">
                            <v-text-field
                                v-model="model"
                                :counter="max"
                                :rules="rules"
                                label="First name"
                            ></v-text-field>
                            <v-slider
                            v-model="max"
                            >
                            </v-slider>
                            </v-form>
                        </v-col>
                    </v-row>
                </v-container>
            </v-row>
            <v-row>
                <p>Элемент</p><p>Элемент</p><p>Элемент</p>
            </v-row>
        </v-col>
    </v-container>
</template>


<script>
  export default {
    data: () => ({
      allowSpaces: false,
      max: 0,
      model: 'Foobar',
    }),

    computed: {
      rules () {
        const rules = []

        if (this.max) {
          const rule =
            v => (v || '').length <= this.max ||
              `A maximum of ${this.max} characters is allowed`

          rules.push(rule)
        }

        if (!this.allowSpaces) {
          const rule =
            v => (v || '').indexOf(' ') < 0 ||
              'No spaces are allowed'

          rules.push(rule)
        }

        if (this.match) {
          const rule =
            v => (!!v && v) === this.match ||
              'Values do not match'

          rules.push(rule)
        }

        return rules
      },
    },

    watch: {
      max: 'validateField',
      model: 'validateField',
    },

    methods: {
      validateField () {
        this.$refs.form.validate()
      },
    },
  }
</script>

<style lang="scss" scoped>
    .calc-cont {
        h1 {
            font-family: Nekst;
            font-style: normal;
            font-weight: 900;
            font-size: 54px;
            line-height: 90%;
        }
    }
</style>