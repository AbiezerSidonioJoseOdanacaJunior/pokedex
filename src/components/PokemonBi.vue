<template>
    <div id="poke">
    <div class="card">
  <div class="card-image">
    <figure>
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
      </div>
      <div class="media-content">
        <p class="title is-4">{{num}} - {{upper(name)}}</p>
        <p class="subtitle is-6">{{ pokemon.type }}</p>
      </div>
    </div>

    <div class="content">
        <button class="button is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
    </div>
  </div>
</div>
</div>
</template>

<script>
import axios from "axios";

export default{
    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front
            console.log(res)
        })
    },
    data(){
        return{
            isFront: true,
            currentImg : '',
            pokemon: {
                type: '',
                front: '',
                back: '',
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String,
    },
    computed:{
         upper(){
            return (v)=>{
              return v.toUpperCase()
              }
           }
     },
     methods: {
        mudarSprite: function(){
        if(this.isFront){
            this.isFront = false;
            this.currentImg = this.pokemon.back;
        }else{
            this.isFront = true;
            this.currentImg = this.pokemon.front;
        }
     }
     }
     
}
</script>
<style>
    #poke{
        margin-top: 1%;
    }
</style>
