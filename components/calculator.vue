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
            <v-row class="values-container">
                <v-col>
                  <p>Сумма договора лизинга</p>
                  <h1>{{ contractSumm }}</h1>
                </v-col>
                <v-col>
                  <p>Ежемесячный платеж</p>
                  <h1>{{monthlyPayment}}</h1>
                </v-col>
            </v-row>
        </v-col>
    </v-container>
</template>


<script>
  export default {
    data: () => ({
      price: 1000000,
      firstRentPercent: 10,
      duration: 1,
      interestRate: 1.5,
    }),

    computed: {
      percentageInterestRate() {
        return this.interestRate / 100;
      },
      monthlyPayment() {
        const p = this.interestRate / 100;
        return Math.round( ( ( this.price - this.firstRentValue ) * ( p + ( p / ( Math.pow( ( 1 + p ), this.duration ) - 1 ) ) ) ) )
      },
      contractSumm() {
        return this.firstRentValue + ( this.duration * this.monthlyPayment );
      },
      firstRentValue() {
        return Math.round( ( this.price / 100 ) * this.firstRentPercent );
      },
      dealSumm() {
        return this.firstRentPercent + duration
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
    .values-container {
      p {
        font-family: Gilroy;
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        line-height: 150%;
        color: #575757;
      }
      h1 {
        font-family: Nekst-Black;
        font-style: normal;
        font-weight: 900;
        font-size: 54px;
        line-height: 90%;
        color: #575757;
      }
    }
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