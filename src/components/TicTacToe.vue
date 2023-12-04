<template>
 
 <div class="toe" v-for="item in items" :key="item.required">
  <div class="block" v-on:click="clickOnKrest"></div>
  <div class="block" v-on:click="clickOnKrest"></div>
  <div class="block" v-on:click="clickOnKrest"></div>
  <div>
    Web Programming React is better
  </div>
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
            }
          }
        }
       },
       KrestAdd(a,b){
         let blocks = document.querySelectorAll(".toe");
            let toe = blocks[a];
            let bl = toe.children[b];
           bl.innerHTML = `<i class="fa-solid fa-x"></i>`;
       }
       ,CircleAdd(a,b){
        let blocks = document.querySelectorAll(".toe");
            let toe = blocks[a];
            let bl = toe.children[b];
           bl.innerHTML = `<i class="fa-regular fa-circle"></i>`;

       }
       ,
       checkWin(){
        let arr = this.items;
  for (let i = 0; i < 3; i++) {
    if (
      (arr[i][0] ===1 && arr[i][1] === 1 && arr[i][2] === 1) ||
      (arr[0][i] === 1 && arr[1][i] === 1 && arr[2][i] ===1)
    ) {
      return true; 
    }
  }


  if (
    (arr[0][0] === 1 && arr[1][1] === 1 && arr[2][2] === 1) ||
    (arr[0][2] === 1 && arr[1][1] === 1 && arr[2][0] === 1)
  ) {
    return true; 
  }

  return false; 
       }
       ,clickOnKrest(e){
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

             
             this.prom();
       }
       ,
       prom(){
      
      this.isKrest();
      setTimeout(()=>{
        if(this.checkWin()){
          alert("1 is win");
        }
      },100);
       
  }
}
  }

  
  
  
</script>

<style scodep>
.block{
  width: 200px;
  height:200px;
  border: 1px solid gray;
  font-size: 100px;
  text-align: center;
}
.block i{
  margin-top: 40px;
}
.toe{
  display: flex;
}
</style>