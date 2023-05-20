<template>
  <div class="listadetarefa">
    <input @keydown.enter="adicionarItem" type="text" v-model="novoItem" class="novaTarefa">
    <button @click="adicionarItem" class="button-adicionar">Adicionar</button>
    <ul>
      <li v-for="(item, index) in lista" :key="index">
        <input type="checkbox" v-model="item.concluido" class="checkbox-lista">
        {{ item.texto }} 
        <button @click="removerItem(index)" class="button-apagar">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  data() {
    return {
      lista: [],
      novoItem: ''
    };
  },

  mounted() {
    this.carregarLista();
  },
  methods: {
    adicionarItem() {
      if (this.novoItem.trim() !== '') {
        this.lista.push({
          texto: this.novoItem,
          concluido: false
        });
        this.novoItem = '';
        this.salvarLista(); // Salvar lista
      }
    },
    removerItem(index) {
      this.lista.splice(index, 1);
      this.salvarLista();
    },
    salvarLista() {
      localStorage.setItem('listaTarefas', JSON.stringify(this.lista));
    },
    carregarLista() {
      const listaSalva = localStorage.getItem('listaTarefas');
      if (listaSalva) {
        this.lista = JSON.parse(listaSalva);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .button-apagar {
    width: 62px;
    height: 20px;
    font-weight: 100;
    background: white;
    padding: 0px 0px;
    border: 1px solid rgb(177, 177, 177);
    border-radius: 4px;
    transition: 0.25s;
  }
  .button-apagar:hover {
    background-color: rgb(201, 201, 201);
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    text-align: left;
  }

.listadetarefa {
  width: 300px;
    height: 435px;
    background-color: rgb(236, 236, 236);
    border: 1px solid rgb(218, 218, 218);
    border-radius: 5px;
    margin-left: 455px;
}

.button-adicionar {
  position: absolute;
    margin-top: -59px;
    height: 23px;
    font-weight: 100;
    margin-left: -32px;
    border: 1px solid rgb(230, 230, 230);
    border-radius: 4px;
}

li {
  display: block;
}

.novaTarefa {
  position: absolute;
    margin-top: -33px;
    border: 1px solid gray;
    margin-left: -151px;
    border-radius: 6px;
    width: 296px;
}
</style>
