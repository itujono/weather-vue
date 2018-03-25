<template>
    <div class="search">
        <div class="search-box">
            <input type="text" class="input" placeholder="Cari tempat..." @input="searchLocation" />
        </div>
        <div class="search-result" v-if="showResult">
            <ul>
                <li v-for="location in locationsArray">{{location.name}}</li>
                <!-- <li>Batam</li> -->
            </ul>
        </div>
    </div>
</template>

<script>
    import { debounce } from "lodash"
    import axios from "axios"

    export default {
        data() {
            return {
                showResult: false,
                locationsArray: []
            }
        },
        methods: {
            searchLocation: _.debounce(function(event) {
                if (event.target.value) {
                    axios.get("http://api.apixu.com/v1/current.json", {
                        params: {
                            key: "d288854f9b8f437fb22173445182503",
                            q: event.target.value
                        }
                    }).then(res => {
                        this.locationsArray = res.data
                        this.showResult = true
                    }).catch(error => {
                        console.log(`Error kali ini dipersembahkan oleh ${error}`)
                        this.showResult = false
                        this.locationsArray = []
                    })
                }
            }, 400)
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
