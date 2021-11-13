<template>
    <BContainer id="app">
        <HomePage v-if="!start" @create="fromNew" @file-loaded="fromFile"></HomePage>
        <div v-else>
            <div v-if="!loading">
                <SetupPage @submit="toNew" v-if="!data"></SetupPage>
                <InvoicePage :data="data" v-else></InvoicePage>
            </div>
            <Load v-else></Load>
        </div>
    </BContainer>
</template>

<script>
import Load from "./components/Load";
import HomePage from "./components/Home";
import SetupPage from "./components/Setup";
import InvoicePage from "./components/Invoice";

export default {
    name: 'App',
    components: {InvoicePage, SetupPage, HomePage, Load},
    data() {
        return {
            loading: false,
            start: false,
            data: null
        }
    },
    methods: {
        fromNew() {
            this.start = true
        },
        fromFile(json) {
            this.data = json
            this.start = true
            this.loading = true
            let self = this
            window.setTimeout(function () {
                self.loading = false
            }, 3000)
        },
        toNew(data) {
            this.data = data
            this.loading = true
            let self = this
            window.setTimeout(function () {
                self.loading = false
            }, 3000)
        }
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
