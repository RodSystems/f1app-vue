<template>
  <div class="corpo">
    <h1 class="centralizado">{{ msg }}</h1>
    <h2>{{ titulo }}</h2>
    <input
      type="search"
      v-on:input="filtro = $event.target.value"
      class="filtro"
      placeholder="Filtre pelo piloto"
    />
    <ul class="lista-pilotos">
      <li v-for="pilotos of pilotoComFiltro" v-bind:key="pilotos.driverId" class="lista-pilotos-item">
        <minha-lista :titulo="formatDriverID(pilotos.driverId)">
          <div>
            <p>
                <b>Nome:</b> <span>{{pilotos.givenName}}&nbsp;{{pilotos.familyName}}</span>
            </p>
            <p>
                <b>Número:</b> <span>{{pilotos.permanentNumber}}</span>
            </p>
            <p>
                <b>Nascimento:</b> <span>{{ formatDate(pilotos.dateOfBirth) }}</span>
            </p>
            <p>
                <b>Nacionalidade:</b> <span>{{pilotos.nationality}}</span>
            </p>
          </div>
        </minha-lista>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Lista from "./shared/lista/Lista";
export default {
  components: {
    "minha-lista": Lista
  },
  name: "F1Screen",
  computed: {
    pilotoComFiltro() {
      if (this.filtro) {
        // filtra a lista, por enquanto vamos retornar uma lista em branco
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.pilotos.filter(pilotos => exp.test(pilotos.driverId));
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        return this.pilotos;
      }
    }
  },
  mounted() {
    axios
      .get("https://ergast.com/api/f1/2019/drivers.json")
      .then(response => {
        this.pilotos = response.data.MRData.DriverTable.Drivers;
      })
      .catch(e => {
        this.erros.push(e);
      });
  },
  methods: {
    reverseMessage() {
      this.titulo = this.titulo
        .split("")
        .reverse()
        .join("");
    },
    formatDate(date) {
      return date.split('-').reverse().join('/')
    },
    formatDriverID(driverId) { 
      return driverId.replace('_',' ')
    }
  },
  data() {
    return {
      filtro: "",
      message: "Olá usuário",
      erros: [],
      pilotos: [],
      titulo: "Filtre pelo piloto"
    };
  },
  props: {
    msg: String
  }
};
</script>

<style scoped>
.centralizado {
  text-align: center;
  color: #333;
}
.corpo {
  font-family: Helvetica, Arial, sans-serif;
  margin: 0 auto;
  width: 96%;
  color: gray;
}
.lista-pilotos {
  list-style: none;
}
.lista-pilotos .lista-pilotos-item {
  display: inline-block;
}
.filtro {
  display: block;
  width: 100%;
  height: 50px;
  font-size: 25px;
}
</style>