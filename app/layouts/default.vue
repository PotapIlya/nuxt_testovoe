<template>
    <div>
        <header class="header">
            <Nav />
        </header>
        <main>
            <Nuxt />
        </main>
    </div>
</template>
<script>
    import Nav from "../components/Nav";
    export default {
        components:{
            Nav
        }
    }
</script>
