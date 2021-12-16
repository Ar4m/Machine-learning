<template>
  <div id="all">
    <h1>Puissance 4</h1>
    <br>
    <div id="container">
        <button class="styleButton" v-on:click="play1">Case 1</button>
        <button class="styleButton" v-on:click="play2">Case 2</button>
        <button class="styleButton" v-on:click="play3">Case 3</button>
        <button class="styleButton" v-on:click="play4">Case 4</button>
        <button class="styleButton" v-on:click="play5">Case 5</button>
        <button class="styleButton" v-on:click="play6">Case 6</button>
        <button class="styleButton" v-on:click="play7">Case 7</button>
        <br>
        <br>
    </div>
  </div>
</template>

<script>
import * as Three from 'three';
export default {
  name: 'Jeu',
  data () {
    return {
      scene:undefined,
      camera:undefined,
      renderer:undefined,
      tab:null,
      tile:null,
      geometry:null,
      baseGrid:null,
      redCoin:null,
      yellowCoin:null,
      played:null,
      AIplayed:null,
      win:null
    }
  },
  methods: {
    init: function() {
        let container = document.getElementById('container');
        let tailleTabx = 7
        let tailleTaby = 6
        this.camera = new Three.PerspectiveCamera(70, container.clientWidth/container.clientHeight, 0.01, 20);
        this.camera.position.z = 5;
        this.camera.position.x = 3,5;
        this.camera.position.y = 2.6;

        this.scene = new Three.Scene();
        this.tab = []
        this.tile = []

        this.geometry = new Three.PlaneGeometry( 1, 1 );
        this.baseGrid = new Three.MeshBasicMaterial( {color: 0xdcf5fd, side: Three.DoubleSide} );
        this.baseGrid2 = new Three.MeshBasicMaterial( {color: 0xe5e5e5, side: Three.DoubleSide} );
        this.redCoin = new Three.MeshBasicMaterial( {color: 0xff0000, side: Three.DoubleSide} );
        this.yellowCoin = new Three.MeshBasicMaterial( {color: 0xd0e000, side: Three.DoubleSide} );
        //generation map


        for (let i = 0; i < tailleTabx; i++) {
          this.tab[i] = []; 
          this.tile[i] = [];
          for (let j = 0; j < tailleTaby; j++) {
            let mat = this.baseGrid
            this.tab[i][j] = 0;
            
            this.tile[i][j] = new Three.Mesh( this.geometry, mat )
            this.scene.add(this.tile[i][j]);
            this.tile[i][j].position.x = i
            this.tile[i][j].position.y = j
          }
        }
        for (let i = 0; i < tailleTabx; i=i+2) {
          for (let j = 0; j < tailleTaby; j=j+2) {
              this.tile[i][j].material = this.baseGrid2
          }
        }
        for (let i = 1; i < tailleTabx; i=i+2) {
          for (let j = 1; j < tailleTaby; j=j+2) {
              this.tile[i][j].material = this.baseGrid2
          }
        }
        

//------------------------------------------------------------------------------------------------------------------
        this.renderer = new Three.WebGLRenderer({antialias: true});
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        container.appendChild(this.renderer.domElement);

    },
    animate: function() {
        requestAnimationFrame(this.animate);
        //this.mesh.rotation.x += 0.01;
        //this.mesh.rotation.y += 0.02;
        this.renderer.render(this.scene, this.camera);
    },

    play1: function(){
        this.addCoin1(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 1")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play2: function(){
        this.addCoin2(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 2")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play3: function(){
        this.addCoin3(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 3")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play4: function(){
        this.addCoin4(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 4")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play5: function(){
        this.addCoin5(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 5")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play6: function(){
        this.addCoin6(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 6")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },
    play7: function(){
        this.addCoin7(1)
        if(this.played == 0){ 
            console.log("placement impossible")
        }
        if(this.played == 1){
            console.log("You played 7")
            this.refreshGrid()
            this.checkWin(1)
            setTimeout(this.AIplay, 500)
        }
    },

    addCoin1: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[0][j] == 0){
                this.tab[0][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin2: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[1][j] == 0){
                this.tab[1][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin3: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[2][j] == 0){
                this.tab[2][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin4: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[3][j] == 0){
                this.tab[3][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin5: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[4][j] == 0){
                this.tab[4][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin6: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[5][j] == 0){
                this.tab[5][j] = player
                this.played = 1
                break
            }
        }
    },
    addCoin7: function(player){
        this.played = 0
        for (let j = 0; j < 6; j++) {
            if(this.tab[6][j] == 0){
                this.tab[6][j] = player
                this.played = 1
                break
            }
        }
    },

    AIplay: function(){
        this.AIplayed = 0

        //check up
        if(this.AIplayed == 0){
            for (let i = 0; i < 7; i++) {
                for (let j = 0; j < 3; j++) {
                    if((this.tab[i][j] == 1 && this.tab[i][j+1] == 1 && this.tab[i][j+2] == 1 && this.tab[i][j+3] == 0)
                    || (this.tab[i][j] == 2 && this.tab[i][j+1] == 2 && this.tab[i][j+2] == 2 && this.tab[i][j+3] == 0))
                    {
                        if(i == 0){ this.addCoin1(2); this.AIplayed = 1; }
                        if(i == 1){ this.addCoin2(2); this.AIplayed = 1; }
                        if(i == 2){ this.addCoin3(2); this.AIplayed = 1; }
                        if(i == 3){ this.addCoin4(2); this.AIplayed = 1; }
                        if(i == 4){ this.addCoin5(2); this.AIplayed = 1; }
                        if(i == 5){ this.addCoin6(2); this.AIplayed = 1; }
                        if(i == 6){ this.addCoin7(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }
        
        //check sides
        if(this.AIplayed == 0){
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 6; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i+1][j] == 1 && this.tab[i+2][j] == 1 && this.tab[i+3][j] == 0 && this.tab[i+3][j-1] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i+1][j] == 2 && this.tab[i+2][j] == 2 && this.tab[i+3][j] == 0 && this.tab[i+3][j-1] !== 0))
                    ){
                        if(i == 0){ this.addCoin4(2); this.AIplayed = 1; }
                        if(i == 1){ this.addCoin5(2); this.AIplayed = 1; }
                        if(i == 2){ this.addCoin6(2); this.AIplayed = 1; }
                        if(i == 3){ this.addCoin7(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }
        if(this.AIplayed == 0){
            for (let i = 3; i < 7; i++) {
                for (let j = 0; j < 6; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i-1][j] == 1 && this.tab[i-2][j] == 1 && this.tab[i-3][j] == 0 && this.tab[i-3][j-1] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i-1][j] == 2 && this.tab[i-2][j] == 2 && this.tab[i-3][j] == 0 && this.tab[i-3][j-1] !== 0))
                    ){
                        if(i == 3){ this.addCoin1(2); this.AIplayed = 1; }
                        if(i == 4){ this.addCoin2(2); this.AIplayed = 1; }
                        if(i == 5){ this.addCoin3(2); this.AIplayed = 1; }
                        if(i == 6){ this.addCoin4(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }

        //check diagonals
        if(this.AIplayed == 0){
            for (let i = 0; i < 4; i++) {
                for (let j = 0; j < 3; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i+1][j+1] == 1 && this.tab[i+2][j+2] == 1 && this.tab[i+3][j+3] == 0 && this.tab[i+3][j+2] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i+1][j+1] == 2 && this.tab[i+2][j+2] == 2 && this.tab[i+3][j+3] == 0 && this.tab[i+3][j+2] !== 0))
                    ){
                        if(i == 0){ this.addCoin4(2); this.AIplayed = 1; }
                        if(i == 1){ this.addCoin5(2); this.AIplayed = 1; }
                        if(i == 2){ this.addCoin6(2); this.AIplayed = 1; }
                        if(i == 3){ this.addCoin7(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }
        if(this.AIplayed == 0){
            for (let i = 3; i < 7; i++) {
                for (let j = 0; j < 3; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i-1][j+1] == 1 && this.tab[i-2][j+2] == 1 && this.tab[i-3][j+3] == 0 && this.tab[i-3][j+2] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i-1][j+1] == 2 && this.tab[i-2][j+2] == 2 && this.tab[i-3][j+3] == 0 && this.tab[i-3][j+2] !== 0))
                    ){
                        if(i == 3){ this.addCoin1(2); this.AIplayed = 1; }
                        if(i == 4){ this.addCoin2(2); this.AIplayed = 1; }
                        if(i == 5){ this.addCoin3(2); this.AIplayed = 1; }
                        if(i == 6){ this.addCoin4(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }
        if(this.AIplayed == 0){
            for (let i = 0; i < 4; i++) {
                for (let j = 3; j < 6; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i+1][j-1] == 1 && this.tab[i+2][j-2] == 1 && this.tab[i+3][j-3] == 0 && this.tab[i+3][j-4] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i+1][j-1] == 2 && this.tab[i+2][j-2] == 2 && this.tab[i+3][j-3] == 0 && this.tab[i+3][j-4] !== 0))
                    ){
                        if(i == 0){ this.addCoin4(2); this.AIplayed = 1; }
                        if(i == 1){ this.addCoin5(2); this.AIplayed = 1; }
                        if(i == 2){ this.addCoin6(2); this.AIplayed = 1; }
                        if(i == 3){ this.addCoin7(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }
        if(this.AIplayed == 0){
            for (let i = 3; i < 7; i++) {
                for (let j = 3; j < 6; j++) {
                    if((this.AIplayed == 0) && (
                       (this.tab[i][j] == 1 && this.tab[i-1][j-1] == 1 && this.tab[i-2][j-2] == 1 && this.tab[i-3][j-3] == 0 && this.tab[i-3][j-4] !== 0)
                    || (this.tab[i][j] == 2 && this.tab[i-1][j-1] == 2 && this.tab[i-2][j-2] == 2 && this.tab[i-3][j-3] == 0 && this.tab[i-3][j-4] !== 0))
                    ){
                        if(i == 3){ this.addCoin1(2); this.AIplayed = 1; }
                        if(i == 4){ this.addCoin2(2); this.AIplayed = 1; }
                        if(i == 5){ this.addCoin3(2); this.AIplayed = 1; }
                        if(i == 6){ this.addCoin4(2); this.AIplayed = 1; }
                        break
                    }
                }
            }
        }

        //play random
        let randomNumber = 0
        while(this.AIplayed == 0){
            randomNumber = (Math.floor(Math.random() * 7))
            if(randomNumber == 0 && this.tab[0][5] == 0){ 
                this.addCoin1(2)
                this.AIplayed = 1
            }
            if(randomNumber == 1 && this.tab[1][5] == 0){ 
                this.addCoin2(2)
                this.AIplayed = 1
            }
            if(randomNumber == 2 && this.tab[2][5] == 0){ 
                this.addCoin3(2)
                this.AIplayed = 1
            }
            if(randomNumber == 3 && this.tab[3][5] == 0){ 
                this.addCoin4(2)
                this.AIplayed = 1
            }
            if(randomNumber == 4 && this.tab[4][5] == 0){ 
                this.addCoin5(2)
                this.AIplayed = 1
            }
            if(randomNumber == 5 && this.tab[5][5] == 0){ 
                this.addCoin6(2)
                this.AIplayed = 1
            }
            if(randomNumber == 6 && this.tab[6][5] == 0){ 
                this.addCoin7(2)
                this.AIplayed = 1
            }
        }
        console.log("AI played "+(randomNumber+1))
        this.refreshGrid()
        this.checkWin(2)
    },

    refreshGrid: function(){
        for (let i = 0; i < 7; i++) {
          for (let j = 0; j < 6; j++) {
            if(this.tab[i][j] == 1){
                this.tile[i][j].material = this.redCoin
            }
            if(this.tab[i][j] == 2){
                this.tile[i][j].material = this.yellowCoin
            }
          }
        }
    },

    checkWin: function(player){
        for (let a = 0; a < 4; a++) {
          for (let b = 0; b < 3; b++) {
            if((this.tab[a][b]==player && this.tab[a+1][b]==player && this.tab[a+2][b]==player && this.tab[a+3][b]==player)
            || (this.tab[a][b]==player && this.tab[a][b+1]==player && this.tab[a][b+2]==player && this.tab[a][b+3]==player)
            || (this.tab[a][b]==player && this.tab[a+1][b+1]==player && this.tab[a+2][b+2]==player && this.tab[a+3][b+3]==player)
            ){ 
                if(player == 1) { alert("You won !") }
                if(player == 2) { alert("AI won...") }
            }
          }
        }
        for (let a = 3; a < 7; a++) {
          for (let b = 3; b < 6; b++) {
            if((this.tab[a][b]==player && this.tab[a-1][b]==player && this.tab[a-2][b]==player && this.tab[a-3][b]==player)
            || (this.tab[a][b]==player && this.tab[a][b-1]==player && this.tab[a][b-2]==player && this.tab[a][b-3]==player)
            || (this.tab[a][b]==player && this.tab[a-1][b-1]==player && this.tab[a-2][b-2]==player && this.tab[a-3][b-3]==player)
            ){ 
                if(player == 1) { alert("You won !") }
                if(player == 2) { alert("AI won...") }
            }
          }
        }
        for (let a = 3; a < 7; a++) {
          for (let b = 0; b < 3; b++) {
            if((this.tab[a][b]==player && this.tab[a-1][b+1]==player && this.tab[a-2][b+2]==player && this.tab[a-3][b+3]==player)
            ){ 
                if(player == 1) { alert("You won !") }
                if(player == 2) { alert("AI won...") }
            }
          }
        }
        for (let a = 0; a < 4; a++) {
          for (let b = 3; b < 6; b++) {
            if((this.tab[a][b]==player && this.tab[a+1][b-1]==player && this.tab[a+2][b-2]==player && this.tab[a+3][b-3]==player)
            ){ 
                if(player == 1) { alert("You won !") }
                if(player == 2) { alert("AI won...") }
            }
          }
        }
    }

  },
  mounted() {
      this.init();
      this.animate();
  }

}
</script>

<style scoped>
  #container{
    width: 1000px;
    height: 700px;
    margin-left: auto;
    margin-right: auto;
  }

  .styleButton{
    padding: 15px 25px 15px 25px;
  }

</style>