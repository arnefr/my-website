
    

<template>
    <div class="dropdown" >
        <div>{{currentItem}}</div>
        <div> <!-- Dropdown Items -->
            <span v-for="item in menuItems" @click="onClick(item)"> {{item}} </span>
        </div>
    </div>
</template>


<script setup>
import { ref } from 'vue';

const menuItems = ref(["Home", "News", "Impressum","Todo","Login"])
const currentItem = ref(menuItems.value[0]);

function onClick(item) {
    currentItem.value = item;
    window.location.hash = item;
}


</script>


<style lang="scss">
*::-webkit-scrollbar {
  width: 50px;
}

*::-webkit-scrollbar-track {
    background-image: url("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSD9iW2bmA5NsUwf7eZoyhJaQoQQBjiO4NsGg&usqp=CAU");
    background-position: center;
    background-size: contain;
  
}

*::-webkit-scrollbar-thumb {
  background-repeat: no-repeat;
  background-position: center;
  background-image: url("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRh072VUuspzYytsXWVUhw-kwS2yzzkxylViw&usqp=CAU");
  background-size: contain;
  border-radius: 20px;}

$border-radius: 5px;

.dropdown {

    @media only screen and (min-width: 1280px) {
        width: 200px;
    }

    @media only screen and (max-width: 1280px) {
        height: 30px;
    }
    position: relative;
    
    > div:first-of-type {
        border: 1px solid gray;
        border-radius: $border-radius;

        background-color: greenyellow;
        color: black;
        width: calc(100% - 2px);
        height: 100%;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    &:hover, &:active {
        animation: test 0.5s;

        > div:first-of-type {
            border-radius: $border-radius $border-radius 0 0;
        }

        > div:last-of-type {
            display: flex;
        }

    }

    > div:last-of-type {
        display: flex;
        flex-direction: column;
        background-color: white;
        color: black;
        border: 1px solid gray;
        border-top: none;
        border-radius: 0 0 $border-radius $border-radius;

        position: absolute;
        left: 0;
        top: 100%;
        right: 0;

        display: none;
        transition: 0.5s;

        > span {
            width: 100%;
            text-align: center;
            cursor: pointer;
            padding: 5px 0;

            &:not(:first-of-type) {
                border-top: 1px solid gray;
            }

            &:hover, &:active {
                background-color: rgba(0, 0, 0, 0.15);
            }
        }
    }

    @keyframes test {
        0% { transform: translate(1px, 1px) rotate(0deg); }
        10% { transform: translate(-1px, -2px) rotate(-1deg); }
        20% { transform: translate(-3px, 0px) rotate(1deg); }
        30% { transform: translate(3px, 2px) rotate(0deg); }
        40% { transform: translate(1px, -1px) rotate(1deg); }
        50% { transform: translate(-1px, 2px) rotate(-1deg); }
        60% { transform: translate(-3px, 1px) rotate(0deg); }
        70% { transform: translate(3px, 1px) rotate(-1deg); }
        80% { transform: translate(-1px, -1px) rotate(1deg); }
        90% { transform: translate(1px, 2px) rotate(0deg); }
        100% { transform: translate(1px, -2px) rotate(-1deg); }
    }
}
</style>