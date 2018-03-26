<template>
    <div class="search">
        <div class="search-box">
            <input type="text" class="input" placeholder="Cari kota nya..." @input="searchLocation" @keyup.esc="clearOut" ref="searchField" />
        </div>
        <div class="search-result" v-if="showResult">
            <ul>
                <li v-for="location in locationsArray" @click="emitLocation(location)">
                    <div class="level">
                        <div class="level-left">
                            <div class="level-item">
                                {{location.name}}
                            </div>
                        </div>
                        <div class="level-right">
                            <div class="level-item">
                                <b-icon icon="plus"></b-icon>
                            </div>
                        </div>
                    </div>
                </li>
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
                    axios.get("http://api.apixu.com/v1/search.json", {
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
            }, 400),
            clearOut() {
                this.showResult = false,
                this.locationsArray = [],
                this.$refs.searchField.value = ""
            },
            emitLocation(location) {
                this.$emit("addLocation", location)
                this.clearOut()
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
        color: #444;
        background-color: rgb(254, 248, 212);
        padding: 10px;
        border-bottom: 1px solid rgb(0, 0, 0, .1);
        cursor: pointer;
    }

    .search-result li:hover {
        background-color: rgba(254, 248, 212, .3);
    }

    .search-result li:hover .level .icon {
        display: flex;
        visibility: visible;
    }

    .search-result li .level .icon {
        display: none;
        visibility: hidden;
        color: rgba(68, 68, 68, .3)
    }
</style>
