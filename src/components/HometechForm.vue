<template>
    <div>
        <Mensage :msg="msg" v-show="msg" />
        <div>
            <form id="homeForm" @submit="createServico">
                <div class="input-container">
                    <label for="nome">Nome do cliente</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="dispositivo">Escolha o dispositivo:</label>
                    <select name="dispositivo" id="dispositivo" v-model="dispositivo">
                        <option value="">Selecione o seu Dispositivo</option>
                        <option v-for="dispositivo in dispositivos" :key="dispositivo.id" :value="dispositivo.tipo">{{dispositivo.tipo}}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="marca">Escolha a marca:</label>
                    <select name="marca" id="marca" v-model="marca">
                        <option value="">Selecione a marca do seu Dispositivo</option>
                        <option v-for="marca in marcas" :key="marca.id" :value="marca.tipo">{{marca.tipo}}</option>
                    </select>
                </div>
                <div id="dispositivos-container" class="input-container">
                    <label id="servico" for="servico">Selecione o serviço</label>
                    <div class="checkbox-container" v-for="servico in servicodata" :key="servico.id" >
                        <input type="checkbox" name="servico" v-model="servicos" :value="servico.tipo">
                        <span>{{servico.tipo}}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Enviar solicitação">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Mensage from './Mensage.vue'


export default {
    name: 'HometechForm',
    components: {
        Mensage
    },
    data (){
        return {
            dispositivos: null,
            marcas: null,
            servicodata: null,
            nome: null,
            dispositivo : null,
            marca : null,
            servicos : [],
            msg: null

        }
    },
    methods: {
        async getAparelhos () {
            const req = await fetch("http://localhost:3000/aparelhos");
            const data = await req.json();


            this.dispositivos = data.dispositivos
            this.marcas = data.marcas
            this.servicodata = data.servicos

        },
        async createServico(e) {
            e.preventDefault();

            const data = {
                nome: this.nome,
                dispositivo: this.dispositivo,
                marca: this.marca,
                servicos: Array.from(this.servicos),
                status: 'Solicitado'
            }

            const dataJson = JSON.stringify(data)

            const req = await fetch("http://localhost:3000/solicitacaoServicos",{
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json()


            this.msg = `Solicitação N: ${res.id} realizada com seucesso!`

            setTimeout(() => this.msg = "", 3000)

            this.nome = '',
            this.dispositivo = '',
            this.marca = '',
            this.servicos = ''
        }
    },
    mounted(){
        this.getAparelhos()
    }
}
</script>

<style scoped>
    #homeForm {
        max-width: 400px;
        margin: 0 auto;
        color: white;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        font-size: 18px;
        padding: 5px 10px;
        border-left: 4px solid #ff0002;
    }

    input, select {
        padding: 10px 10px;
        width: 400px;
        
    }


    #dispositivos-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #servico {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;

    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: white;
        color: #141414;
        padding: 10px;
        font-size: 18px;
        font-weight: bold;
        cursor: pointer;
        transition: .5s;  
    }

    .submit-btn:hover {
        background-color: transparent;
        border: 2px solid #ff0002;
        color: white;
        box-shadow: 1px 1px 20px 2px #ff0002;
    }

</style>
