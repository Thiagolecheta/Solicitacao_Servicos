<template>
    <div>
        <Banner />
        <div class="main-container">
            <h1>Faça sua solicitação<br> de serviço:</h1>
        <HometechForm />
        </div>
    </div>
</template>

<script>

import Banner from '../components/Banner.vue'
import HometechForm from '../components/HometechForm.vue'

export default {
    name: 'Home',
    components: {
        Banner,
        HometechForm
    }
}
</script>
