<template>
    <div id="nav">
        <router-link to="/" id="logo_url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Serviços</router-link>
  </div>
</template>

<script>

export default {
    name: 'NavBar',
    props: ['logo','alt']
}
</script>


<style scoped>
    #nav{
        background-color: #141414;
        border-bottom: 2px solid #ff0002;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        padding: 15px 50px;
    }

    #nav #logo_url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 100px;
        height: 100px;
    }

    #nav a {
        color: white;
        text-decoration: none;
        font-size: 19px;
        margin: 12px;
        transition: .5s;
    }

    #nav a:hover {
        color: #ff0002;
    }
</style>