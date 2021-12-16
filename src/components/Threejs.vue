<template>
  <div id="all">
    <h1> Dijkstra</h1>
    <div id="container"></div>
  </div>
</template>

<script>
import * as Three from 'three';
export default {
  name: 'Dijkstra',
  data () {
    return {
      scene:undefined,
      camera:undefined,
      renderer:undefined
    }
  },
  methods: {
    init: function() {
        let container = document.getElementById('container');
        let tailleTab = 16
        this.camera = new Three.PerspectiveCamera(70, container.clientWidth/container.clientHeight, 0.01, 20);
        this.camera.position.z = 15;
        this.camera.position.x = tailleTab/2;
        this.camera.position.y = tailleTab/2;

        this.scene = new Three.Scene();
        let tab =[]
        let tile = []

        const geometry = new Three.PlaneGeometry( 1, 1 );
        const terre = new Three.MeshBasicMaterial( {color: 0x32CD32, side: Three.DoubleSide} );
        const lave = new Three.MeshBasicMaterial( {color: 0xed0000, side: Three.DoubleSide} );
        //generation map

        for (let i = 0; i < tailleTab; i++) {
          tab[i] = []; 
          tile[i]=[];
          for (let j = 0; j < tailleTab; j++) {
            let mat = terre
            tab[i][j] = "terre";
            if(Math.floor(Math.random() * 3)==0){ 
              mat = lave
              tab[i][j] = "lave";
            }
            tile[i][j] = new Three.Mesh( geometry, mat )
            this.scene.add(tile[i][j]);
            //console.log(i + "  " +j)
            tile[i][j].position.x = i
            tile[i][j].position.y = j
          }
        }

        let xkey = Math.floor(Math.random() * tailleTab)
        let ykey = Math.floor(Math.random() * tailleTab)
        tab[xkey][ykey] = "key" 
        tile[xkey][ykey].material = new Three.MeshBasicMaterial( {color: 0xffff00, side: Three.DoubleSide} );
        //generation hero
        let x = xkey 
        let y = ykey
        while(x == xkey && y == ykey){
          x = Math.floor(Math.random() * tailleTab)
          y = Math.floor(Math.random() * tailleTab)
        }
        tab[x][y] = "Hero" 
        tile[x][y].material = new Three.MeshBasicMaterial( {color: 0xf4fefe, side: Three.DoubleSide} );

        function HighlightCheckCase(scene,tiletab,colortile){
          for (let i = 0; i < tiletab.length; i++) {
            const geometry = new Three.PlaneGeometry( 0.7, 0.7 );
            const mat = new Three.MeshBasicMaterial( {color: colortile, side: Three.DoubleSide} );
            const plane = new Three.Mesh( geometry, mat )
            scene.add(plane);
            plane.position.x = tiletab[i][0]
            plane.position.y = tiletab[i][1]
          }
        }

        //Solution :
        console.log("clé : "+[xkey,ykey]);
        console.log("héro : "+[x,y]);

        let tabToVerify = [[x, y]]
        let tabVerified = []
        let keyFound = false
        let itération = 0

        while(tabToVerify.length > 0) {
          
          itération++

          checkTile(tabToVerify[0])
          tabVerified.push(tabToVerify[0])
          tabToVerify.shift()
          
          for (let index = 0; index < tabVerified.length; index++) {
            if(shallowEqual(tabVerified[index],[xkey,ykey])){
              keyFound = true
            }
          }
          if(keyFound){
            console.log("Nombre d'itérations : "+itération)
            console.log("Clé trouvée")
            break
          }
        }

        if(!keyFound){
          console.log("Nombre d'itérations : "+itération)
          console.log("Clé non atteinte")
        }


        function checkTile([tabx, taby]){
        //tile right :
          let rightAlreadyVerified = false                                    // Pour chacune des 4 cases à vérifier,
          for (let index0 = 0; index0 < tabVerified.length; index0++) {       // cette partie du code sert à : 
              if(shallowEqual(tabVerified[index0],[tabx+1,taby])){            // - Récupérer les éléments de tabVerified et tabToVerify
                rightAlreadyVerified = true                                   //  qui sont des objets et non des tableaux (dans mon code)
              }                                                               // - Les comparer un par un aux coordonnées de la 
            }                                                                 //  case à vérifier
          for (let index0 = 0; index0 < tabToVerify.length; index0++) {       // - Changer la valeur de la variable "alreadyVerified"
              if(shallowEqual(tabToVerify[index0],[tabx+1,taby])){            //  si la case est déjà dans un des "tab"
                rightAlreadyVerified = true                                   //
              }                                                               //
            }                                                                 
          if(tabx+1 >= 0 && tabx+1 <= 15 && tab[tabx+1][taby] != "lave" && !rightAlreadyVerified){    // Et cette partie sert à ajouter la case
            tabToVerify.push([tabx+1,taby])                                                           // dans tabToVerify si toutes les conditions
          }                                                                                           // sont valides
        //tile down :
          let downAlreadyVerified = false
          for (let index1 = 0; index1 < tabVerified.length; index1++) {
            if(shallowEqual(tabVerified[index1],[tabx,taby-1])){
              downAlreadyVerified = true
            }
          }
          for (let index1 = 0; index1 < tabToVerify.length; index1++) {
            if(shallowEqual(tabToVerify[index1],[tabx,taby-1])){
              downAlreadyVerified = true
            }
          }
          if(taby-1 >= 0 && taby-1 <= 15 && tab[tabx][taby-1] != "lave" && !downAlreadyVerified){
            tabToVerify.push([tabx,taby-1])
          }
        //tile left :
          let leftAlreadyVerified = false
          for (let index2 = 0; index2 < tabVerified.length; index2++) {
            if(shallowEqual(tabVerified[index2],[tabx-1,taby])){
              leftAlreadyVerified = true
            }
          }
          for (let index2 = 0; index2 < tabToVerify.length; index2++) {
            if(shallowEqual(tabToVerify[index2],[tabx-1,taby])){
              leftAlreadyVerified = true
            }
          }
          if(tabx-1 >= 0 && tabx-1 <= 15 && tab[tabx-1][taby] != "lave" && !leftAlreadyVerified){
            tabToVerify.push([tabx-1,taby])
          }
        //tile up :
          let upAlreadyVerified = false
          for (let index3 = 0; index3 < tabVerified.length; index3++) {
            if(shallowEqual(tabVerified[index3],[tabx,taby+1])){
              upAlreadyVerified = true
            }
          }
          for (let index3 = 0; index3 < tabToVerify.length; index3++) {
            if(shallowEqual(tabToVerify[index3],[tabx,taby+1])){
              upAlreadyVerified = true
            }
          }
          if(taby+1 >= 0 && taby+1 <= 15 && tab[tabx][taby+1] != "lave" && !upAlreadyVerified){
            tabToVerify.push([tabx,taby+1])
          }

        }

        HighlightCheckCase(this.scene, tabVerified, 0x1E90FF)

        function shallowEqual(object1, object2) {
          const keys1 = Object.keys(object1);
          const keys2 = Object.keys(object2);
          if (keys1.length !== keys2.length) {
            return false;
          }
          for (let key of keys1) {
            if (object1[key] !== object2[key]) {
              return false;
            }
          }
          return true;
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

</style>