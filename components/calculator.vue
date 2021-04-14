<template>
    <v-container class="calc-cont" fluid>
        <v-text-field v-bind:options='{inputMask:"(###) ### ## ##"}'>
        </v-text-field>
        <v-col>
            <h1 class="mb-16">
                    Рассчитайте стоимость <br> автомобиля в лизинг
            </h1>

                    <div
                    class="d-flex flex-column flex-lg-row"
                    >
                        <v-col
                            cols="12"
                            lg="4"
                            class="input-cuntainer"
                        >
                              <v-form ref="form">
                                <p class="mb-8">Стоимость автомобиля</p>
                                <v-text-field
                                    color="orange"
                                    class="custom-text-field disabled-custom-field"
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
                                track-color="#E1E1E1"
                                track-fill-color="#FF9514"
                                color="#FF9514"
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
                            lg="4"
                            class="input-cuntainer"
                        >
                              <v-form ref="form">
                                <p class="mb-8">Первоначальный взнос</p>
                                <v-text-field
                                    color="orange"
                                    class="custom-text-field"
                                    height='68px'
                                    outlined
                                    hide-details
                                    readonly
                                    v-model="firstRentValue"
                                >
                                <h2
                                slot="append"
                                >{{firstRentPercent}}%</h2>
                                </v-text-field>
                                <v-slider
                                track-color="#E1E1E1"
                                track-fill-color="#FF9514"
                                color="#FF9514"
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
                            lg="4"
                            class="input-cuntainer"
                        >
                              <v-form ref="form" >
                                <p class="mb-8">Срок лизинга</p>
                                <v-text-field
                                    color="orange"
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
                                track-color="#E1E1E1"
                                track-fill-color="#FF9514"
                                color="#FF9514"
                                class="custom-slider"
                                :min="1"
                                :max="60"
                                v-model="duration"
                                >
                                </v-slider>
                              </v-form>
                        </v-col>
                    </div>
            <v-row class="values-container mb-16">
                <v-col class="mb-5">
                  <p class="mb-8">Сумма договора лизинга</p>
                  <h1>{{ formatedContractSumm }}</h1>
                </v-col>
                <v-col class="mb-5">
                  <p class="mb-8">Ежемесячный платеж</p>
                  <h1>{{ formatedMonthlyPayment }}</h1>
                </v-col>
                <v-col class="d-flex align-center">
                  <template>
                    <v-row>
                      <v-dialog
                        v-model="dialog"
                        width="100%"
                      >

                        <template v-slot:activator="{ on, attrs }">
                          <v-btn rounded dark color="#ff9514" class="make-form-btn" v-bind="attrs" v-on="on">Оставить заявку</v-btn>
                        </template>

                        <v-card>
                          <v-card-title>
                            <span class="headline mb-8 header-text"><p class="header-text">Онлайн-заявка</p></span>
                          </v-card-title>
                          <v-card-subtitle class="">
                            <span>Заполните форму, и мы вскоре свяжемся с вами, чтобы ответить на все вопросы</span>
                          </v-card-subtitle>
                          <v-card-text>
                            <v-container>
                              <v-row>
                                
                                <v-col cols="12">
                                  <v-text-field
                                    label="Email*"
                                    required
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12">
                                  <v-text-field
                                    label="Password*"
                                    type="password"
                                    required
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-container>
                            <small>*indicates required field</small>
                          </v-card-text>
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn
                              color="blue darken-1"
                              text
                              @click="dialog = false"
                            >
                              Close
                            </v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
                    </v-row>
                  </template>
                </v-col>
            </v-row>
        </v-col>
        
    </v-container>
</template>


<script>
  export default {
    
    data: () => ({
      dialog: false,
      price: 1000000,
      firstRentPercent: 10,
      duration: 1,
      interestRate: 1.5,
      calcVal: ''
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
      formatedContractSumm() {
        return `${new Intl.NumberFormat().format(this.contractSumm)} ₽`
      },
      formatedMonthlyPayment() {
        return `${new Intl.NumberFormat().format(this.monthlyPayment)} ₽`
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
      calcVal: 'doCalc'
    },

    methods: {
      doCalc() {
        console.log(this.$refs.inp)
      }
    },
  }
</script>

<style lang="scss" scoped>
    
    .make-form-btn {
      box-shadow: none !important;
      height: 68px !important;
      padding: 14px 70px 18px 70px !important;
      font-family: Nekst;
      font-style: normal;
      font-weight: 900;
      font-size: 30px !important;
      line-height: 36px;
      text-transform: none !important;
      border-radius: 200px;
    }
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
          border: none;
          background-color: #F3F3F4;
          border-radius: 10px;

          .v-text-field__slot {
            height: 10000px;
          }
          h2 {
            font-family: Nekst;
            font-style: normal;
            font-weight: 900;
            font-size: 30px;
            color: #575757;
          }

        
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