<template>
  <div>
    <section class="section">
      <div class="container">
        <div class="columns janela-principal">
          <div class="column is-3 lista-de-conversas">
            <div class="barra-superior" />
            <div
              class="item"
              v-for="(conversa, index) in conversas"
              :key="conversa"
              @click="indiceAtivo = index"
            >
              <div class="title is-6">{{ conversa.usuario }}</div>
              <div class="subtitle is-6">Ultima Mensagem....</div>
            </div>
          </div>
          <div class="column conversa-ativa">
            <div class="barra-superior">
              <span>{{ conversas[indiceAtivo].usuario }}</span>
            </div>
            <div class="lista-mensagens">
              <mensagem
                v-for="(mensagem, indice) in conversas[indiceAtivo].mensagens"
                :key="indice"
                :conteudo="mensagem.conteudo"
                :horario="mensagem.horario"
                :verde="mensagem.verde"
              />
            </div>
            <div class="barra-inferior">
              <input
                type="text"
                class="input"
                v-on:keyup.enter="enviarMensagem"
                placeholder="Insira sua mensagem"
                v-model="conteudoASerEnviado"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import conversaIniciais from "./dados.js";
import mensagem from "./mensagem.vue";
export default {
  data: function () {
    return {
      conversas: conversaIniciais,
      indiceAtivo: 0,
      conteudoASerEnviado: "",
    };
  },
  components: {
    mensagem,
  },
  methods: {
    enviarMensagem: function () {
      let horarioAtual = new Date().getHours() + ":" + new Date().getMinutes();
      let novaMensagem = {
        horario: horarioAtual,
        conteudo: this.conteudoASerEnviado,
        verde: true,
      };
      this.conversas[this.indiceAtivo].mensagens.push(novaMensagem);
      this.conteudoASerEnviado = "";
    },
  },
};
</script>

<style>
.janela-principal {
  min-height: 1200px;
  box-shadow: 0 3rem 3rem -1rem rgba(10, 10, 10, 0.2);
}
.barra-inferior {
  bottom: 0;
  width: 77%;
  padding: 10px;
  position: absolute;
  background: #f0f0f0;
}
.lista-mensagens {
  height: 85%;
  display: flex;
  justify-content: flex-end;
  flex-direction: column;
}
.columns {
  min-height: 750px;

  box-shadow: 0 3rem -1rem rgba(10, 10, 10, 0.2);
}

.column {
  padding: 0;
}

.lista-de-conversas {
  background-color: white;
}
.conversa-ativa {
  padding: 0;
  background: #e5ddd5;
  position: relative;
}

.barra-superior {
  margin: 0;
  height: 50px;
  background: #ededed;
  border-right: 1px solid #e1e1e1;
  border-bottom: 1px solid rgb(200, 200, 200);
}

.barra-superior span {
  line-height: 50px;
  margin-left: 25px;
  font-weight: 500;
}

.item {
  border-bottom: 1px solid #f2f2f2;
  padding: 15px 30px;
  margin-bottom: 0 !important;
}

.subtitle {
  color: grey;
}

.item:hover {
  background: #f5f5f5;
  cursor: pointer;
}
</style>
