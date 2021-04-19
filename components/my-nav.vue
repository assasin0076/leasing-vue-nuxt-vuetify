<template>
    <v-container fluid >
        <v-app-bar app flat color="white" class="nav-content-container clls"  >

            <div class=" container-logo d-flex justify-space-between align-center">
                <v-btn text href="/">
                    <img src="/img/LeasingCar.svg" alt="">
                    <img src="/img/LeasingCar-1.svg" alt="">
                </v-btn>
                <v-divider
                    class="d-none d-md-flex"
                    inset
                    vertical
                ></v-divider>
                <p class="d-none d-md-flex">лизинговая компания</p>
            </div>
            

            <v-spacer />
            
            <div class="text-center">
                <v-dialog
                v-model="dialog"
                width="500"
                transition="dialog-top-transition"
                >
                <template v-slot:activator="{ on, attrs }">
                    <v-btn
                    class="d-lg-none"
                    color="#2A3B4D"
                    icon
                    v-bind="attrs"
                    v-on="on"
                    >
                        <v-icon dark>
                            mdi-menu
                        </v-icon>
                    </v-btn>
                </template>

                <v-card class='burger-menu'>
                    <v-card-title class="headline lighten-2 float-right">
                    <v-btn
                        class="float-right"
                        color="#2A3B4D"
                        icon
                        @click="dialog = false"
                    >
                        <v-icon dark>
                            mdi-close
                        </v-icon>
                    </v-btn>
                    </v-card-title>

                    <v-card-text class="burger-menu-elements-container">
                        <v-list class="">
                            <v-col>
                                <v-list-item
                                v-for="(item, index) in navItems.filter((el) => !especialyButtons.includes(el.title))"
                                :key="index"
                                >
                                <v-list-item-title class="simple-button">
                                    <v-btn v-bind="item.attr" class="simple-button">{{ item.title }}
                                    </v-btn>
                                </v-list-item-title>
                                </v-list-item>
                            </v-col>
                            <v-col>
                                <v-list-item
                                v-for="(item, index) in navItems.filter((el) => especialyButtons.includes(el.title))"
                                :key="index"
                                >
                                <v-list-item-title class="d-flex justify-center"><v-btn rounded dark color="#ff9514" class="special-button">{{ item.title }}</v-btn></v-list-item-title>
                                </v-list-item>
                            </v-col>

                        </v-list>
                    </v-card-text>


                    <v-card-actions>
                    <v-spacer></v-spacer>
                    
                    </v-card-actions>
                </v-card>
                </v-dialog>
            </div>
            <div class="text-center nav-elements-container d-none d-lg-flex">
                <div class="d-flex flex-row">
                    <div 
                    v-for="(item, index) in navItems"
                    :key="index"
                    >
                        <div>
                            <v-btn v-if="item.type == 'btn'" v-bind="item.attr">
                                {{ item.title }}
                            </v-btn>
                            <v-menu v-if="item.type == 'droping'" open-on-hover offset-y>
                                <template v-slot:activator="{ on, attrs }">
                                    <v-btn
                                    text
                                    v-bind="attrs"
                                    v-on="on"
                                    >
                                        {{ item.title }}
                                    </v-btn>
                                </template>

                                <v-list>
                                    <v-list-item
                                    v-for="(innerItem, index) in item.inner"
                                    :key="index"
                                    >
                                        <v-list-item-title>
                                            <v-btn v-bind='innerItem.attr'>
                                                {{ innerItem.title }}
                                            </v-btn>
                                            
                                        </v-list-item-title>
                                    </v-list-item>
                                </v-list>
                            </v-menu>
                        </div>
                    </div>
                </div >
            </div>
            
        </v-app-bar>
    </v-container>    
</template>

<script>
  export default {
    props: {
        width: Number,
    },
    breakpoint: {
            thresholds: {
            xs: 320,
            sm: 768,
            md: 1024,
            lg: 1440,
            },
            scrollBarWidth: 24,
    },
    data: () => ({
        especialyButtons: ['Оставить заявку'],
        navItems: [
            {
                type: 'droping',
                title: 'Лизинг',
                attr: { 
                    text: true,
                    vBind:"attrs",
                    vOn:"on"
                    },
                inner: [
                    { title: 'Для личного использования', attr: { text: true } },
                    { title: 'Для юредических лиц', attr: { text: true } },
                    { title: 'Калькулятор', attr: { text: true, href: 'calculatorPage' } },
                ]
            },
            { type: 'btn', title: 'Каталог', attr: { text: true, href: '/' } },
            { type: 'btn', title: 'О нас', attr: { text: true, href: 'contacts' } },
            { type: 'btn', title: 'Оставить заявку', attr: { outlined: true, rounded: true, color: "#ff9514", class: "special-button", href: '/' } },
        ],
        dialog: false,
    }),
    methods: {
        showWidth() {
            console.log(this.width);
        }
    },
  }
</script>

<style lang="scss" scoped>
    .special-button {
        padding: 22px 20px !important;
    }
    .v-btn {
        text-transform: none;
    }
    .nav-elements-container {
       .v-btn {
            font-family: Gilroy;
            font-style: normal;
            font-weight: bold;
            font-size: 16px;
            line-height: 24px;
            color: #575757;
        } 
    }
    .burger-menu {
        position: absolute;
        top: 0px;
        right: 0px;
        width: 340px;
        height: 610px;
        .burger-menu-elements-container {
            padding: 2px 2px !important;
            height: 90%;
            .v-list {
                width: 100%;
                flex-wrap: wrap;
                display: flex;
                align-content: space-between;
            }
            .simple-button {
                font-family: Gilroy;
                font-style: normal;
                font-weight: bold;
                font-size: 24px;
                line-height: 24px;
                padding: 0px;
            }
            .special-button {
                font-family: Gilroy;
                font-style: normal;
                font-weight: bold;
                font-size: 16px;
                line-height: 24px;
            }
            display: flex;
        }
    }
    .container-logo {
        width: 400px;
        .butt-list {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        p {
            margin-bottom: 0px !important;
            font-family: Gilroy;
            font-style: normal;
            font-weight: normal;
            font-size: 16px;
            line-height: 150%;

            letter-spacing: 0.92px;
            text-transform: lowercase;

            color: rgba(17, 17, 17, 0.5)
        }
        .v-btn {
            padding: 0px 0px !important;
        }
    }
    
</style>