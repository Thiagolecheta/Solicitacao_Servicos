<template>
    <div id="dispositivos-table">
        <div>
            <Mensage :msg="msg" v-show="msg" />
            <div id="dispositivos-table-header">
                <div class="order-id">:#</div>
                <div>Cliente</div>
                <div>Dispositivo:</div>
                <div>Marca dispositivo:</div>
                <div>Serviço</div>
                <div>Status</div>

            </div>
        </div>
        <div id="dispositivos-table-row">
            <div class="dispositivos-table-row" v-for="solicitacaoServico in solicitacaoServicos" :key="solicitacaoServico.id">
                <div class="order-number">{{solicitacaoServico.id}}</div>
                <div>{{solicitacaoServico.nome}}</div>
                <div>{{solicitacaoServico.dispositivo}}</div>
                <div>{{solicitacaoServico.marca}}</div>
                <div>
                    <ul>
                        <li v-for="(servico, index) in solicitacaoServico.servicos" :key="index">{{servico}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateSolicitacao($event, solicitacaoServico.id)">
                        <option value="">Selecione</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="solicitacaoServico.status == s.tipo">
                            {{s.tipo}}
                        </option>
                    </select>
                    <button class="btn-delete"  @click="cancelarSolicitacao(solicitacaoServico.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>    
</template>

<script>

import Mensage from './Mensage.vue'

export default {
    
    name: 'Dashboard',
    data(){
        return {
            solicitacaoServicos: null,
            solicitacao_id: null,
            status: [],
            msg: null
        }
    },
    components: {
        Mensage
    },
    methods: {
        async getServico(){
            const req = await fetch('http://localhost:3000/solicitacaoServicos')
            const data = await req.json()

            this.solicitacaoServicos = data

            this.getStatus()
        },
        
        async getStatus() {
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json()

            this.status = data
        },
        async cancelarSolicitacao(id){
            const req = await fetch(`http://localhost:3000/solicitacaoServicos/${id}`, {
                method: "DELETE"
            });

            const res = await req.json()


            this.msg = `Solicitação CANCELADA!`

            setTimeout(() => this.msg = "", 3000)


            this.getServico()
            

        },
        async updateSolicitacao(event, id){

            const option = event.target.value;

            const dataJSON = JSON.stringify({status:option})

            const req = await fetch (`http://localhost:3000/solicitacaoServicos/${id}`, {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: dataJSON
            });

            const res = await req.json()

            this.msg = `A Solicitação N: ${res.id} foi atualizado para ${res.status}!`

            setTimeout(() => this.msg = "", 3000)


            

        }
    },
    mounted() {
        this.getServico()
    }
}
</script>


<style scoped>

    #dispositivos-table {
        color: white;
        max-width: 1200px;
        margin: 0 auto;

    }

    #dispositivos-table-row,
    #dispositivos-table-header,
    .dispositivos-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #dispositivos-table-header {
        font-weight: bold;
        font-size: 16px;
        padding: 20px;
        border-bottom: 4px solid #ff0002;
    }
    
    #dispositivos-table-header div,
    .dispositivos-table-row div {
        width: 19%;
    }
    .dispositivos-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 2px solid #ff0002;
    }

    #dispositivos-table-header .order-id,
    .dispositivos-table-row .order-number {
        width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }
    
    .btn-delete {
        background-color: #ff0002;
        color: white;
        margin-top: 5px;
        padding: 10px;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        transition: .5s;  
    }

    .btn-delete:hover {
        background-color: transparent;
        border: 2px solid #ff0002;
        color: white;
        box-shadow: 1px 1px 20px 2px #ff0002;
    }
</style>   