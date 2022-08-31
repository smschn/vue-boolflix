<template>
    <header>
        <h1>BOOLFLIX</h1>
        <div>
            <input type="text" v-model="whatToSearch" placeholder="Digita per cercare un film." />
            <button @click="$emit('searchThis', whatToSearch)">Cerca</button>
        </div>
    </header>
</template>

<script>
export default {
    name: 'MyHeader',
    data() {
        return {
            whatToSearch: ''
        }
    }
}
</script>

<style lang='scss'>
@import '../styles/vars.scss';

header {
    height: 80px;
    background-color: $bg_h;
    color: $bg_c1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px;

    input,
    button {
        padding: 10px;   
    }

    button {
        background-color: $bg_c1;
        border-color: $bg_c1;
        color: #fff;
    }

}
</style>