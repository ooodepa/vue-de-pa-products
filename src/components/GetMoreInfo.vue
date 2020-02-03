<template>
<div>
    <h2>{{ array[index]['gsx$наименование']['$t'] }}</h2>
    <img :src=" array[index]['gsx$imgsrc']['$t']" alt="">
    <table>
        <tr>
            <td>Модель:</td>
            <td>{{ array[index]['gsx$код']['$t'] }}</td>
        </tr>
        <tr>
            <td>Цена за 1 ед. c НДС:</td>
            <td>{{ array[index]['gsx$цена']['$t'] }}</td>
        </tr>
        <tr>
            <td>В коробке, шт.:</td>
            <td>{{ array[index]['gsx$вкоробке']['$t'] }}</td>
        </tr>
        <tr>
            <td>Вес товара:</td>
            <td>{{ array[index]['gsx$kg']['$t'] }}</td>
        </tr>
        <tr>
            <td>Вес 1-ой штуки:</td>
            <td>{{ array[index]['gsx$kg1']['$t'] }}</td>
        </tr>
    </table>
</div>
</template>

<script>
export default {
    props: {
        index: Number,
        array: Array
    },
}
</script>
