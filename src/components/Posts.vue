<template>
<div class="hello">
    <div class="posts">

        <div class="post" v-for="(element, index) in array" :key="index" v-on:click="getIndex(index)">
            <!-- <p>{{ element['gsx$наименование']['$t'] }}</p> -->
            <img :src="element['gsx$imgsrc']['$t']" alt="">
            <p>Модель: <b>{{ element['gsx$код']['$t'] }}</b></p>
            <p>Цена за 1 ед. c НДС: <b>{{ element['gsx$цена']['$t'] }}</b></p>
            <p>В коробке, шт.: <b>{{ element['gsx$вкоробке']['$t'] }}</b></p>

        </div>

        <div class="more-info" id="close" style="display: none;">
            <div class="block">

                <div class="header">
                    <button v-on:click="close">X</button>
                </div>

                <div class="body">
                    <GetMoreInfo
                        v-bind:index="clickedIndex"
                        v-bind:array="array"
                    />
                </div>

            </div>
        </div>

    </div>
</div>
</template>

<script>
import axios from 'axios'

import GetMoreInfo from '@/components/GetMoreInfo.vue'

export default {
    name: 'HelloWorld',
    props: {
        google_table_id: String,
        google_table_list: String
    },
    data() {
        return {
            array: [
                {
                    gsx$наименование: { $t: null },
                    gsx$imgsrc: { $t: null },
                    gsx$код: { $t: null },
                    gsx$цена: { $t: null },
                    gsx$вкоробке: { $t: null },
                    gsx$kg: { $t: null },
                    gsx$kg1: { $t: null },
                }
            ],
            clickedIndex: 0
        };
    },
    methods: {
        getData() {
            axios(`https://spreadsheets.google.com/feeds/list/${this.google_table_id}/${this.google_table_list}/public/values?alt=json`)
                .then(e => {
                    this.array = e.data.feed.entry
                })
        },
        getIndex(index) {
            document.getElementById("close").style = "display: block;"
            this.clickedIndex = index
        },
        close() {
            document.getElementById("close").style = "display: none;"
        }
    },
    mounted() {
        this.getData();
    },
    components: {
        GetMoreInfo
    }
}
</script>

<style scoped>
.posts {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.posts .post {
    width: 160px;
    border: 1px solid #212529;
    border-radius: 8px;
    margin: 8px;
    padding: 16px;
}

.posts .more-info {
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
}

.posts .more-info .block {
    width: calc(100% - 4 * 16px);
    height: calc(100% - 4 * 16px);
    background-color: white;
    margin: 16px;
    padding: 16px;
    border-radius: 8px;
    overflow: auto;
}
</style>
