<template>
    <div class="spare-parts">
        <div class="spare-parts__hotspot">
            <div class="spare-parts__quantity">
                <h2>Forward <br /> deflector shields</h2>
                <button class="add" v-on:click="increaseItems">+</button>
                <button class="total">{{ totalitems }}</button>
                <button class="remove" v-on:click="decreaseItems">-</button>
            </div>
            <div class="spare-parts__add-to-cart">
                <button class="cart" v-on:click="addToCart">Add to cart</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "SpareParts",
        props: ['totalitems'],
        methods: {
            increaseItems() {
                this.$emit('increase-items')
            },
            decreaseItems() {
                this.$emit('decrease-items')
            },
            addToCart() {
                this.$emit('add-to-cart', 'totalItems')
            },
        },
    }

</script>

<style scoped lang="scss">

    $mobile-side-margin: 10px;
    $desktop-side-margin: 20px;

    .spare-parts {
        width: 100%;
        height: 100vh;
        background: url("http://stefankarlberg.se/wp-content/uploads/2019/11/falcon.jpg");
        background-repeat: no-repeat;
        background-position: center center;
        background-size: cover;

        &__hotspot {
            right: 20%;
            top: 10%;
            height: 250px;
            width: 250px;
            border-radius: 50%;
            position: absolute;
            background: rgba(27, 60, 3, 0.93);
        }

        &__quantity {
            margin-top: 20px;
            padding: 10px;
        }

    h2 {
        margin-bottom: 20px;
        font-size: 17px;
        color: white;
        line-height: 20px;
        text-transform: uppercase;
        font-family: arial;
        }

    button {
        padding: 5px $mobile-side-margin;
        margin: 0px;
        color: white;
        background: none;
        border: 1px solid white;
        font-size: 17px;
        list-style: 17px;



        @media (min-width: 480px) {
            padding-left: $desktop-side-margin;
            padding-right: $desktop-side-margin;
            }
        }

        .cart {
            color: black;
            background: white;
        }



    &__add-to-cart {
         margin-top: 20px;


    }
    }
</style>