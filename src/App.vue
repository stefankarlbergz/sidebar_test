<template>
    <div id="app">
        <div class="main">

            <div v-if="currentComponent === 'SpareParts'" class="checkout">Checkout {{ cart }}</div>
            <component
                    :is="currentComponent"
                    v-bind:totalitems=totalItems
                    v-bind:starships=starships
                    @decrease-items=decreaseItems(1)
                    @increase-items=increaseItems(1)
                    @add-to-cart=addToCart(totalItems)
                    @loadComponent1="loadComponent('SpareParts')"
            >
            </component>
        </div>

        <div class="overlay" @click="closeMenu()"></div>
        <div class="sidebar">
            <button @click="toggleMenu()">{{ sidebarToggleLabel }}</button>
            <ul class="sidebar__menu">
                <li>
                    <a href="#" @click="loadComponent('Home'), toggleMenu()">Home</a>
                </li>
                <li>
                    <a href="#" @click="loadComponent('SpareParts'), toggleMenu()">Order spareparts</a>
                </li>
            </ul>
        </div>
    </div>


</template>

<script>
    import Home from './components/Home.vue'
    import SpareParts from './components/SpareParts.vue'
    import axios from 'axios'
    import $ from "jquery";

    export default {
        name: 'app',
        components: {
            Home,
            SpareParts
        },
        data: function () {
            return {
                label: 'Open',
                isOpen: false,
                currentComponent: "Home",
                totalItems: 12,
                cart: 0,
                starships: null,
            }
        },
        mounted() {
            axios
                .get('https://swapi.co/api/starships/')
                .then(response => {
                    this.starships = response.data['results']
                })
                .catch(error => {
                    window.console.log(error)
                    this.errored = true
                })
                .finally(() => this.loading = false)
        },
        computed: {
            /*  changeLabel() {
                if  ($('#app').hasClass('is-open')){
                  window.console.log('open')
                  return `${this.label}`
                } else {
                  window.console.log('close')
                  return `${this.label}`
                }
              }*/
            sidebarToggleLabel() {
                return this.isOpen ? 'Close' : 'Open'
            }
        },
        methods: {
            openMenu() {
                this.isOpen = true
                $('body').addClass('sidebar-open')
            },
            closeMenu() {
                this.isOpen = false
                $('body').removeClass('sidebar-open')
            },
            toggleMenu() {
                if (this.isOpen) {
                    this.closeMenu()
                } else {
                    this.openMenu()
                }
            },
            loadComponent(component) {
                this.currentComponent = component;
            },
            increaseItems(number) {
                this.totalItems += number;
            },
            decreaseItems(number) {
                this.totalItems -= number;
            },
            addToCart(number) {
                this.cart += number;
            }
        }
    }
</script>

<style lang="scss">

    body {
        margin: 0 !important;
        padding: 0 !important;
        background-image: url("https://c.wallhere.com/photos/15/78/1920x900_px_1star_action_adventure_Awakens_Disney_fi_Force-1622101.jpg!d");
        background-size: 180%;
        background-repeat: no-repeat;
    }

    #app {
        margin-top: 60px;
    }


    .checkout {
        position: absolute;
        height: 60px;
        width: 98%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        font-size: 20px;
        text-transform: uppercase;
        letter-spacing: 0.6px;
        font-family: arial;
        color: green;


    }

    .overlay {
        top: 0;
        left: 0;
        height: 100%;

        .sidebar-open & {
            background: #000000c4;
            transition: ease-in-out 0.8s;
            height: 100vh;
            width: 100%;
            position: absolute;
        }
    }

    //
    // Sidebar
    // ---------------------------

    .sidebar {
        position: fixed;
        top: 0;
        left: 0;
        height: 100%;
        padding: 30px;
        width: 300px;
        background: black;
        color: white;
        transform: translateX(-80%);
        transition: ease-in-out 0.4s;
        border-right: 1px solid green;
        display: flex;
        justify-content: center;
        align-items: center;

        .sidebar-open & {
            transform: translateX(0%);
        }

        & button,
        & button:focus {
            color: green;
            background: none;
            border: none;
            position: absolute;
            right: 0;
            top: 0;
            margin-top: 60px;
            font-size: 18px;
            transform: rotate(-90deg);
            text-transform: uppercase;
            transition: ease-in-out 0.4s;
            letter-spacing: 3px;
            outline: 0;
        }

        & ul {
            font-size: 17px;
            text-decoration: none;
            list-style-type: none;
            font-family: arial;
            text-transform: uppercase;
            margin-top: 150px;

            & li a {
                display: block;
                height: 40px;
                text-decoration: none;
                color: white;
            }

            & li:hover {
                color: red;
            }
        }
    }


    /*

    .sidebar {
      display: flex;
      align-self: center;
      position: fixed;
      padding: 30px;
      width: 300px;
      height: 100vh;
      border-right: 1px solid green;
      background: black;
      color: white;
      transform: translateX(-80%);
      transition: ease-in-out 0.4s;
      pointer-events: auto;

      & button,
      & button:focus {
        width: 120px;
        height: 30px;
        color: green;
        background: none;
        border: none;
        position: absolute;
        right: 0;
        top: 0;
        margin-right: -20px;
        margin-top: 60px;
        font-size: 18px;
        transform: rotate(-90deg);
        text-transform: uppercase;
        transition: ease-in-out 0.4s;
        letter-spacing: 3px;
        outline: 0;
      }
    }


    */


    .main {
        width: 100%;
        height: 100%;
        display: block;
        position: absolute;
        left: 0;
        top: 0;
        transition: ease-in-out 0.4s;
        text-align: center;
        color: red;
    }
</style>
