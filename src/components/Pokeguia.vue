<template>
    <div class="background">
        <img :src="require('../assets/images/pokemon.png')" class="pokeheader"/>
        <h3>PokeGuía</h3>
        <form @submit.prevent="buscar(pokenombre)">
            <div class="form-group text-white">
                <label for="buscarPokemon">Ingresa el nombre de un Pokémon</label>
                <input type="text" class="form-control" v-model="pokenombre">
            </div>
            <button type="submit" class="btn btn-primary bg-warning">¡Buscar!</button>
        </form>
        <section class="resultado">
            <img :src="imagen" alt="">
            <h4>Habilidades</h4>
                <ul>
                    <li v-for="(item, index) in habilidades" :key="index">{{item.ability.name}}</li>
                </ul>
            <h4>Movimientos</h4>
                <ul>
                    <li v-for="(item, index) in movimientos" :key="index">{{item.move.name}}</li>
                </ul>
        </section>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Pokeguia',
    data(){
        return {
            pokenombre: '',
            imagen: '',
            habilidades: [],
            movimientos: [],
        }
    },
    methods: {
        buscar(pokemon){
            if(pokemon){
                axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
                .then(json => {
                    this.imagen = json.data.sprites.front_default,
                    this.movimientos = json.data.moves,
                    this.habilidades = json.data.abilities
                })
                .catch(error => console.log(error))
            }
        }
        },
        created() {
            this.pokenombre = 'pikachu',
            this.buscar(this.pokenombre);
        },
        
    }
</script>

<style>
.background {
    background-image: url('../assets/images/background.jpeg');
    background-size: cover;
    background-attachment: fixed;  
}
.pokeheader {
  width: 500px;
  display: block;
  margin: 0 auto;
  padding-top: 60px;
}
h3 {
  text-align: center;
  color: white;
}
form {
  width: 50%;
  display: block;
  margin: 0 auto;
  margin-top: 60px;
}
.resultado {
    text-align: center;
    padding-bottom: 50px;
}
li {
    list-style: none;
}
</style>