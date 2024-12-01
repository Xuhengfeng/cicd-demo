<template>
    <div>
        <a href="https://vitejs.dev" target="_blank">
            <img src="/vite.svg" class="logo" alt="Vite logo" />
        </a>
        <a href="https://vuejs.org/" target="_blank">
            <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
        </a>
        <button @click="getUsers">get请求</button>
        <p v-for="item in state.usersList">{{ item }}</p>
        <h1>xhf聊前端</h1>
        <chartPie :series-data="dataList" :extra-option="extraOption" />
    </div>
    <!-- <HelloWorld msg="Vite + Vue" /> -->
</template>
<script setup>
import { reactive } from 'vue';
import HelloWorld from './components/HelloWorld.vue';
import chartPie from './components/echart/pie/chartPie.vue';
const dataList = [
    { name: 'Vue', value: 20 },
    { name: 'React', value: 20 },
    { name: 'Angular', value: 20 },
];
const extraOption = {
  color: ["#fe883a", "#2d90d1", "#f75981", "#90e2a9"],
}

const baseURL = "http://localhost:3005"; 
const axiosInstance = axios.create({
    headers: { "Content-Type": "application/json" },
    baseURL,
    timeout: 3000,
});

// https://xuhengfeng.github.io/cicd-demo/
const state = reactive({
    usersList: [],
});
const getUsers = async (params) => {
    const result = await axiosInstance.get("/user/init-data");
    state.usersList = result.data.data;
    console.log(state);
}
</script>

<style scoped>
div {
  width: 100vw;
  height: 100vh;
}
.logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
}
.logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
    filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
