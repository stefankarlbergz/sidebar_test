<template>
    <div class="starship">
        <h1>Welcome to Starship Junkyard</h1>
        <div class="starship-wrapper">
            <div class="starship-wrapper__card" v-for="item in starships" :key="item.model">
                <div class="starship-wrapper__card__overlay">
                    <h3><a href="#" v-on:click="loadComponent">{{ item.name }}</a></h3>
                    <h4>{{ item.model}}</h4>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Home",
        props: ['starships'],
        methods: {
            loadComponent() {
                this.$emit('loadComponent1')
                window.console.log('test')
            }
        },
    }
</script>

<style scoped lang="scss">

    .starship {
        width: 80%;
        margin-left: auto;
        margin-right: auto;

    h1 {
        font-family: arial;
        text-transform: uppercase;
        letter-spacing: 3px;
        font-weight: 300;
        font-size: 40px;
        margin-top: 100px;
        margin-bottom: 100px;
        color: green;
        }
    }

    .starship-wrapper {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;

    &__card {
         display: flex;
         align-items: flex-end;
         width: 300px;
         height: 200px;
         margin: 10px;
         border: 1px solid green;
         background: black;

    &__overlay {
         height: 100%;
         width: 100%;
         display: flex;
         flex-direction: column;
         align-items: center;
         justify-content: center;

    &:hover {
         background: green;
     }

    h3 a {
        font-size: 25px;
        font-family: arial;
        text-transform: uppercase;
        color: white;
        margin-bottom: 0px;
        text-decoration: none;
    }

    h4 {
        font-size: 12px;
        font-family: arial;
        color: white;
        margin-top: 0px;
    }
    }
    }
    }


    .sidebar-open {
        position: fixed;
        overflow: hidden;

    .main {}
    .sidebar {}
    }

</style>