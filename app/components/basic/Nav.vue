<template>
    <div class="container">
        <ul v-if="arrayNav.length"
            class="header__list col-12 col-lg-8 ml-auto d-flex align-items-center justify-content-between">

            <li
                    v-for="(item, index) in arrayNav"
                    :key="index"
            >
                <nuxt-link
                        class="header__list-item"
                        :to="item.path">
                    {{ item.name }}
                </nuxt-link>
            </li>


        </ul>
    </div>
</template>

<script>
    export default {
        name: "Nav",
        data: () => ({
            arrayNav: [
                { name: 'Личный кабинет', path: '/' },
                { name: 'Раздел 1', path: '/' },
                { name: 'Раздел 2', path: '/' },
                { name: 'Раздел 3', path: '/' },
                { name: 'Раздел 4', path: '/' },
                { name: 'Раздел 5', path: '/' },
            ]
        })
    }
</script>

