
<template>

    <div class="navbar">
        <div>
            <h1>My Cool Website</h1>
        </div>
        <div>
            <div><NavMenu></NavMenu></div>
            <div class="searchbox">
                <input v-model="msg" placeholder="Search" />
                <button></button>
            </div>
        </div>
    </div>
</template>


<script setup>
import { ref } from 'vue';
import NavMenu from './NavMenu.vue';


</script>


<style lang="scss">
.navbar {
    background-color: #444;
    height: 100px;
    color: white;
    display: flex;
    flex-direction: column;
    position: relative;
    z-index: 1000;

    >div {
        flex-grow: 1;


        &:first-of-type {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        &:last-of-type {
            display: flex;
            justify-content: space-between;
            padding: 5px;
        }
    }
    .searchbox {
        background-color: aqua;
        display: flex;

        input {
            padding: 5px;
            border-radius: 0;
            border: none;
        }

        button{
            border: none;
            border-radius: 0;
            background-image:url("https://www.nicepng.com/png/full/553-5538821_black-city-backpack-350-lupe-icon-ohne-hintergrund.png");
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            background-origin: content-box;
            padding: 10px;
            width: 50px;

            &:hover{
                background-color: #9e9e9e;
                cursor: poi;
            }
        }
        
    }

}
</style>
