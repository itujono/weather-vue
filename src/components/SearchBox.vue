<template>
    <div class="search">
        <div class="search-box">
            <b-input v-model="search" placeholder="Cari tempat..."></b-input>
        </div>
        <div class="search-result">
            <ul>
                <li>Batam</li>
                <li>Surabaya</li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {

            }
        }
    }
</script>

<style>
    .search-result {
        text-align: left;
        margin-bottom: 1em;
    }

    .search-result li {
        background-color: rgb(254, 248, 212);
        padding: 10px;
        border-bottom: 1px solid rgb(0, 0, 0, .1);
    }
</style>
