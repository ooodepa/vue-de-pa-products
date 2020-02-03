<template>
    <nav class="menu">
        <ul>
            <li>
                <a href="https://de-pa.by">Вернуться на сайт</a>
            </li>
            <li v-for="(element, index) in menu" :key="index">
                <router-link :to="element['href']">{{ element['name'] }}</router-link>
            </li> 
        </ul>
    </nav>
</template>

<script>
export default {
    data() {
        return {
            menu: [
                {
                    name: 'Английская серия',
                    href: '/british-system-series'
                },
            ]
        }
    }
}
</script>