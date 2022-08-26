
<template>

    <div class="navbar">
        <div>
            <h1>My Cool Website</h1>
        </div>
        <div>
            <div><NavMenu></NavMenu></div>
            <div class="searchbox">
                <input v-model="mySearchContent" placeholder="Search" @keydown.enter="funcSearch" />
                <button @click="funcSearch" type="submit"></button>
            </div>
        </div>
    </div>
</template>


<script setup>

import { ref } from 'vue';
import NavMenu from './NavMenu.vue';
const mySearchContent = ref ('')
function funcSearch () {
    const myurl = new URL("https://de.wikipedia.org/w/index.php")
    myurl.searchParams.append("search", mySearchContent.value)
    window.location.href = myurl.toString()
    
}

</script>


<style lang="scss">

.navbar {
    background-color: #444;
    color: white;
    display: flex;
    flex-direction: column;
    position: relative;
    z-index: 1000;

    > div {
        flex-grow: 1;


        &:first-of-type {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 5px;
        }

        &:last-of-type {
            display: flex;
            justify-content: space-between;
            gap: 5px;
            padding: 5px;

            @media only screen and (max-width: 1280px) {
                flex-direction: column-reverse;
            }
        }
    }
    .searchbox {
        display: flex;

        input {
            padding: 5px;
            border-radius: 0;
            border: none;
            width: 100%;
        }

        button{
            border: none;
            border-radius: 0;
            background-image:url("https://www.nicepng.com/png/full/553-5538821_black-city-backpack-350-lupe-icon-ohne-hintergrund.png");
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            background-origin: content-box;
            padding: 5px;
            width: 50px;

            &:hover{
                background-color: #9e9e9e;
                cursor: poi;
            }
        }
        
    }

}
</style>
