<template>
 <div class="tic_tac">
 <div class="toe" v-for="item in items" :key="item.required">
  <div class="block" id = "true" v-on:click="clickOnKrest"></div>
  <div class="block" id = "true" v-on:click="clickOnKrest"></div>
  <div class="block" id = "true" v-on:click="clickOnKrest"></div>
</div>


<div class="okoshka none">
  <div class="textW">{{winner}} </div>
  <button class="close" v-on:click="closeWin"><i class="fa-solid fa-x"></i></button>
</div>
<button class=" reset" v-on:click="resetClik"> reset</button>
</div>
 


</template>

<script>
  export default{
    props:{
        items:{
          type: Array,
          required: true
        }
    },data(){
      return{
          Krest:true,
          winner:""
      }
    }
    ,methods:{
       isKrest(){
         let arr = this.items;
        for(let i = 0;i<arr.length;i++){
          for(let j = 0;j<3;j++){
            if(arr[i][j]==1){
             this.KrestAdd(i,j);
            }else if(arr[i][j]==0){
            this.CircleAdd(i,j);
            }else{
               this.remove(i,j);
            }
          }
        }
       },
       remove(a,b){
        let blocks = document.querySelectorAll(".toe");
            let toe = blocks[a];
            let bl = toe.children[b];
           bl.innerHTML = ``;
           bl.id = "true";
       },
       KrestAdd(a,b){
         let blocks = document.querySelectorAll(".toe");
            let toe = blocks[a];
            let bl = toe.children[b];
           bl.innerHTML = `<i class="fa-solid fa-x" id = "k"></i>`;
       }
       ,CircleAdd(a,b){
        let blocks = document.querySelectorAll(".toe");
            let toe = blocks[a];
            let bl = toe.children[b];
           bl.innerHTML = `<i class="fa-regular fa-circle" id = "z"></i>`;

       }
       ,
       checkWin(){
        let arr = this.items;
  for (let i = 0; i < 3; i++) {
    if (
      (arr[i][0] ===1 && arr[i][1] === 1 && arr[i][2] === 1) ||
      (arr[0][i] === 1 && arr[1][i] === 1 && arr[2][i] ===1) || ((arr[i][0] ===0 && arr[i][1] === 0 && arr[i][2] === 0) ||
      (arr[0][i] === 0 && arr[1][i] === 0 && arr[2][i] ===0))
    ) {
      return true; 
    }
  }
  if (
    (arr[0][0] === 1 && arr[1][1] === 1 && arr[2][2] === 1) ||
    (arr[0][2] === 1 && arr[1][1] === 1 && arr[2][0] === 1) || ((arr[0][0] === 0 && arr[1][1] === 0 && arr[2][2] === 0) ||
    (arr[0][2] === 0 && arr[1][1] === 1 && arr[2][0] === 0))
  ) {
    return true; 
  }

  return false; 
       },checkDraw(){
        let arr = this.items;
        let dr = true;
        for(let i = 0;i<3;i++){
          for(let j = 0;j<3;j++){
            if(arr[i][j]=="j"){
              dr =false;
            }
          }
         
        }
        return dr;
       }
       ,clickOnKrest(e){
        if(e.target.id == "true"){
          e.target.id = "false";
        let a =0;
            let b = 0;
            let arr = this.items;
            let btn = e.target;
            let toe = btn.parentNode ;
            let blocks = toe.parentNode;
             for(let i = 0;i<3;i++){
               if(blocks.children[i]===toe){
                a = i;
               } 
               if(toe.children[i]===btn){
                b = i;
               }
              }

          if(this.Krest){
               arr[a][b] = 1;
               this.Krest = !this.Krest;
              
              }else{
              arr[a][b] = 0;
              this.Krest = !this.Krest;
             }

              console.log(arr);
             this.prom();
       }
      }
       ,
       prom(){
        let block = document.querySelectorAll(".block");
         this.winner = `winner is ${this.Krest?'green':'yellow'}`;
         let oko = document.querySelector(".okoshka");
      this.isKrest();
      setTimeout(()=>{
        if(this.checkWin()){
          oko.classList.remove("none");
          for(let i = 0;i<block.length;i++){
            block[i].classList.add("isfin");
          }
         
        }else if(this.checkDraw()){
          oko.classList.remove("none");
          this.winner = "draw";
        }
      },100);
       
  },
  resetClik(){
    this.Krest = true;
    let btn = this.items;
    let block = document.querySelectorAll(".block");
    for(let i = 0;i<3;i++){
      for(let j = 0;j<3;j++){
         btn[i][j] = "j";
      }
    }
    for(let i = 0;i<block.length;i++){
            block[i].classList.remove("isfin");
          }
    this.prom();
  }
  ,
  closeWin(){
    let oko = document.querySelector(".okoshka");
    oko.classList.add("none");
  }
}
  }

  
  
  
</script>

<style scodep>
body{
  background-color: rgb(43, 91, 163);
}
.block{
  width: 200px;
  height:200px;
  border: 10px solid gray ;
  font-size: 100px;
  text-align: center;
}
.isfin{
  pointer-events: none;
}
.block i{
  margin-top: 40px;
}
.toe{
  display: flex;
  margin: 0 auto;
}
#k{
  color: rgb(221, 162, 24);
}
#z{
  color: rgb(91, 210, 164);
}

.tic_tac{
  width: 600px;
  margin: 0 auto;
  position: relative;
 
}

.reset{
  position: absolute;
  top: 200px;
  right:-150px;
  padding: 10px 20px;
  color: #fff;
  font-size: 20px;
  cursor: pointer;
  border: none;
  background-color: rgb(227, 18, 18);
  border-radius: 3px;
  transition: all .3s;
}
.reset:hover{
  background-color: rgb(228, 54, 54);
}

.okoshka{
  top: 20%;
  right: -200px;
  z-index: 2;
 width: 1000px;
 height: 300px;
 background-color: #fff;
 text-align: center;
 position: absolute;
 background-color: rgb(135, 138, 222);
}
.textW{
  font-size: 80px;
  color: rgb(91, 34, 6);
  margin-top: 100px;
}
.close{
  position: absolute;
  right: 30px;
  top: 30px;
  color: rgb(235, 24, 24);
  border: none;
  background-color: rgb(135, 138, 222);
  font-size: 30px;
  cursor: pointer;
}
.none{
  display: none;
}
</style>