<template>
    <div>
        <header class="header d-none d-sm-block">
            <Nav />
        </header>
        <main class="mt-4 mt-sm-0">
            <Nuxt />
        </main>
    </div>
</template>
<script>
    import Nav from "../components/basic/Nav";
    export default {
        components:{
            Nav
        }
    }
</script>
