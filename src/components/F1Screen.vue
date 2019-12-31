<template>
  <div class="corpo">
    <h1 class="centralizado">{{ msg }}</h1>
    <h2>{{ titulo }}</h2>
    <input
      type="search"
      v-on:input="filtro = $event.target.value"
      class="filtro"
      placeholder="filtre pelo piloto"
    />
    <ul class="lista-pilotos">
      <li v-for="pilotos of pilotoComFiltro" v-bind:key="pilotos.driverId" class="lista-pilotos-item">
        <minha-lista :titulo="pilotos.driverId">
          <div>
            <p>
                Nome:<span>{{pilotos.givenName}}&nbsp;{{pilotos.familyName}}</span>
            </p>
          </div>
          <div>
            <p>
                Número:<span>{{pilotos.permanentNumber}}</span>
            </p>
          </div>
           <div>
            <p>
                Nascimento:<span>{{pilotos.dateOfBirth}}</span>
            </p>
          </div>
           <div>
            <p>
                Nacionalidade:<span>{{pilotos.nationality}}</span>
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
}
</style>