<template>
    <main>
        <div class="container">
            <div class="card">prova</div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'MyMain'
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';

main {
    height: calc(100vh - 80px);
    background-color: $bg_m;
    padding: 30px;

    .container {
        width: 80%;
        margin: auto;
    }
}

</style>