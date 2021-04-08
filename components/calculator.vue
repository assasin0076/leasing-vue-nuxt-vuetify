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
                            class="input-cuntainer"
                        >
                              <v-form ref="form">
                                <p>Стоимость автомобиля</p>
                                <v-text-field
                                    class="custom-text-field"
                                    height='68px'
                                    type="number"
                                    outlined
                                    hide-details
                                    v-model="price"
                                    :counter="max"
                                >
                                <h2
                                slot="append"
                                >₽</h2>
                                </v-text-field>
                                <v-slider
                                :min='1000000'
                                :max='6000000'
                                class="custom-slider"
                                v-model="price"
                                >
                                </v-slider>
                              </v-form>
                        </v-col>
                        <v-col
                            cols="12"
                            md="4"
                            class="input-cuntainer"
                        >
                              <v-form ref="form">
                                <p>Первоначальный взнос</p>
                                <v-text-field
                                    class="custom-text-field"
                                    height='68px'
                                    outlined
                                    hide-details
                                    v-model="firstRentValue"
                                    :counter="max"
                                >
                                <h2
                                slot="append"
                                >{{firstRentPercent}}%</h2>
                                </v-text-field>
                                <v-slider
                                class="custom-slider"
                                :min="10"
                                :max="60"
                                v-model="firstRentPercent"
                                >
                                </v-slider>
                              </v-form>
                        </v-col>
                        <v-col
                            cols="12"
                            md="4"
                            class="input-cuntainer"
                        >
                              <v-form ref="form">
                                <p>Срок лизинга</p>
                                <v-text-field
                                    class="custom-text-field"
                                    height='68px'
                                    outlined
                                    hide-details
                                    v-model="duration"
                                    :counter="max"
                                    :rules="rules"
                                >
                                <h2
                                slot="append"
                                >мес.</h2>
                                </v-text-field>
                                <v-slider
                                class="custom-slider"
                                :min="1"
                                :max="60"
                                v-model="duration"
                                >
                                </v-slider>
                              </v-form>
                        </v-col>
                    </v-row>
                </v-container>
            </v-row>
            <v-row>
                <v-col>
                  <p>Сумма договора лизинга</p>
                  <h2>4461313</h2>
                </v-col>
                <v-col>
                  <p>Сумма договора лизинга</p>
                  <h2>{{x}}</h2>
                </v-col>
            </v-row>
        </v-col>
    </v-container>
</template>


<script>
  export default {
    data: () => ({
      x: 99999,
      allowSpaces: false,
      max: 0,
      price: 1000000,
      firstRentPercent: 10,
      duration: 1,
    }),

    computed: {
      firstRentValue() {
        return Math.round(this.price / 100 * this.firstRentPercent);
      },
      rules () {
        const rules = []

        if (this.max) {
          const rule =
            v => (v || '').length <= this.max ||
              `A maximum of ${this.max} characters is allowed`

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
    .input-cuntainer {
      .custom-text-field {
          font-family: Nekst;
          font-style: normal;
          font-weight: 900;
          font-size: 30px;

        h2 {
          font-family: Nekst;
          font-style: normal;
          font-weight: 900;
          font-size: 30px;
        }

        border: none;
        background-color: #F3F3F4;
        border-radius: 10px;
      }
      .custom-slider {
        position: relative;
        top: -16px;
      }
    }
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