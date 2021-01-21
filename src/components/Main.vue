<template>
  <div id="container">
    <header>
      <h1>Covid-19</h1>      
    </header>
    <div class="entrada">
      <input type="text" v-model="paisPesquisado" />    
      <button @click="getOne">&#128270;</button>
    </div>
    <div class="container-grid" v-for="item in teste" :key="item.pais">
      <div class="card">
        <h2>Confirmado</h2>        
        <p>{{ item.totalConfirmado }}</p>
      </div>
      <div class="card">
        <h2>Mortes</h2>
        <p>{{ item.totalMortes }}</p>
      </div>
      <div class="card">
        <h2>Recuperados</h2>
        <p>{{ item.recuperado }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from "axios";

export default {
  async created() {
    await this.getAllData(), this.tratarGet() , this.getOne()
  },
  data() {
    return {
      requestOfAll: [],
      tratado: [],
      paisPesquisado: "Brazil",
      pais: [],
      teste: [],
    };
  },
  methods: {
    async getAllData() {
      const { data } = await Axios.get("https://api.covid19api.com/summary");
      return (this.requestOfAll = data.Countries);
    },
    tratarGet() {
      this.requestOfAll.forEach((e) => {
        this.tratado.push({
          pais: e.Country,
          totalConfirmado: e.TotalConfirmed,
          totalMortes: e.TotalDeaths,
          recuperado: e.TotalRecovered,
        });
      });
    },
    getOne() {
      this.tratado.find((e) => {
        if (e.pais == this.paisPesquisado) {
          this.teste = [];
          this.teste.push(e);          
        }
      });
    },
  },
};
</script>

<style scoped>

  #container {
    width: 400px;
    background: rgba(255, 255, 255, 0.25);
    box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    border-radius: 10px;
  }

  .entrada{
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }

  .entrada input{
    border: none;
    border-radius: 20px 0 0 20px;
    width: 125px;
    height: 20px;
    text-align: center;
  }
  
  .entrada button{
    border: none;
    background-color:rgb(255, 255, 255);
  }

  header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    margin-bottom: 20px;
  }

  header h1 {
    margin-top: 20px;
    margin-bottom: 0px;
    font-size: 3rem;
    text-align: center;
    color: white;
    text-shadow: 3px 2px 10px rgba(0, 0, 0, 0.411);
  }

  .container-grid{
    display: grid;
    grid-template-columns: 50% 50%;
  }

  .container-grid div:last-child{
    margin-left:55%;
  }

  .card {
    background: rgba(255, 255, 255, 0.25);
    box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    width: 88%;
    text-align: center;
    margin: 10px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.575);
    border-radius: 20px;
  
  }

  .card p {
    font-size: 1.2rem;
  }

  @media screen and (max-width:400px){
    .container-grid{
      justify-content: center;
      grid-template-columns: 100%;
    }

    .container-grid div{
      margin: 10px auto;
    }

    .container-grid div:last-child{
      margin:10px auto 20px auto;
    }

  }
</style>
