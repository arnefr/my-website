<template>
    <div class="wrapper">
        <div class="content">
            <div v-if="currentPage == '#News'">
                <News></News>
            </div>
            <div v-else-if="currentPage == '#Impressum'">
                <Impressum></Impressum>
            </div>
            <div v-else-if="currentPage == '#Todo'">
                <Todo></Todo>
            </div>
            <div v-else-if="currentPage == '#Login'">
                <Login></Login>
            </div>
            <div v-else>
                <Home></Home>
            </div>
        </div>
        <div class="footer">© by arne August 2022. All rights reserved.</div>
    </div>
</template>

<script setup>
import { computed, ref, onMounted } from 'vue';
import Home from './Home.vue';
import Impressum from './Impressum.vue';
import News from './News.vue';
import Todo from './Todo.vue';
import Login from './Login.vue';

const currentPage = ref("")

onMounted(() => {
    window.addEventListener("hashchange", () => {
        currentPage.value = window.location.hash
    })
})

</script>

<style lang="scss">
.wrapper {
    width: 1280px;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    height: calc(100vh - 100px);
    margin: 0 auto;
    box-shadow: 0px 0px 5px 3px rgba(0, 0, 0, 0.45);


    .footer {
        padding-top: 50px;
        padding-bottom:  25px;
        text-align: center;
    }
    .content {
        padding: 25px;
        overflow-y: auto;
    }
}
</style>