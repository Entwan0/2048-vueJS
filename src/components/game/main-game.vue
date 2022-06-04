<template v-on:keyup="keyHandler($event)">
  <h1>2048</h1>

  <table>
    <tr v-for="colonne in rowInTable" v-bind:key="colonne">
      <td v-for="ligne in rowInTable" v-bind:key="ligne" onmousedown="return false"  v-bind:class="
      { two: valueTable[colonne][ligne] === 2,
        four: valueTable[colonne][ligne] === 4,
        eight: valueTable[colonne][ligne] === 8,
        sixteen: valueTable[colonne][ligne] === 16,
        thirtyTwo: valueTable[colonne][ligne] === 32
      }">
        <div v-if="valueTable[colonne][ligne] !== 0">
          {{valueTable[colonne][ligne]}}
        </div>
      </td>
    </tr>
  </table>

</template>

<script>
export default {
  name: 'main-Game',
  data () {
    return {
      nbrRow: 4,
      rowInTable: [],
      valueTable: [],
      rowOfZero: [],
    }
  },

  created : function () {
    window.addEventListener('keydown', function (e) {
      let isDeplaced = false;
      switch (e.key){

        case 'ArrowUp':
        case 'z':
          for(let i = 1;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                let s=0;
                if((i-3 >=0) && this.isEmpty(i-3,j)){
                  s=3;
                }
                else if((i-2 >=0) && this.isEmpty(i-2,j)){
                  s=2;
                }
                else if((i-1 >=0) && this.isEmpty(i-1,j)){
                  s=1;
                }

                if(s !==0){
                  this.valueTable[i-s][j] = this.valueTable[i][j];
                  this.valueTable[i][j] = 0;
                  console.log("deplace")
                  isDeplaced = true;
                }
              }
            }
          }

          for(let i = 1;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                if (this.valueTable[i - 1][j] === this.valueTable[i][j]) {
                  this.valueTable[i - 1][j] = this.valueTable[i - 1][j] * 2;
                  this.valueTable[i][j] = 0;
                  console.log("fusion")
                  isDeplaced = true
                }
              }
            }
          }
          break;

        case 'ArrowLeft':
        case 'q':
          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 1; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                let s=0;
                if((j-3 >=0) && this.isEmpty(i,j-3)){
                  s=3;
                }
                else if((j-2 >=0) && this.isEmpty(i,j-2)){
                  s=2;
                }
                else if((j-1 >=0) && this.isEmpty(i,j-1)){
                  s=1;
                }

                if(s !==0){
                  this.valueTable[i][j-s] = this.valueTable[i][j];
                  this.valueTable[i][j] = 0;
                  isDeplaced = true;
                }
              }
            }
          }

          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 1; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                if (this.valueTable[i][j - 1] === this.valueTable[i][j]) {
                  this.valueTable[i][j - 1] = this.valueTable[i][j - 1] * 2;
                  this.valueTable[i][j] = 0;
                  console.log("fusion")
                  isDeplaced = true
                }
              }
            }
          }

          console.log("left")
          break;

        case 'ArrowRight':
        case 'd':
          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                let s=0;
                if((j+3 <this.nbrRow) && this.isEmpty(i,j+3)){
                  s=3;
                }
                else if((j+2 <this.nbrRow) && this.isEmpty(i,j+2)){
                  s=2;
                }
                else if((j+1 <this.nbrRow) && this.isEmpty(i,j+1)){
                  s=1;
                }

                if(s !==0){
                  this.valueTable[i][j+s] = this.valueTable[i][j];
                  this.valueTable[i][j] = 0;
                  isDeplaced = true;
                }
              }
            }
          }

          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                if ((j + 1 <= 3) && this.valueTable[i][j + 1] === this.valueTable[i][j]) {
                  this.valueTable[i][j + 1] = this.valueTable[i][j + 1] * 2;
                  this.valueTable[i][j] = 0;
                  console.log("fusion");
                  isDeplaced = true;
                }
              }
            }
          }

          console.log("right")
          break;

        case 'ArrowDown':
        case 's':
          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if (!this.isEmpty(i, j)) {
                let s = 0;
                if ((i + 3 < this.nbrRow) && this.isEmpty(i + 3, j)) {
                  s = 3;
                } else if ((i + 2 < this.nbrRow) && this.isEmpty(i + 2, j)) {
                  s = 2;
                } else if ((i + 1 < this.nbrRow) && this.isEmpty(i + 1, j)) {
                  s = 1;
                }

                if (s !== 0) {
                  this.valueTable[i + s][j] = this.valueTable[i][j];
                  this.valueTable[i][j] = 0;
                  isDeplaced = true
                }
              }
            }
          }

          for(let i = 0;i<this.nbrRow;i++) {
            for (let j = 0; j < this.nbrRow; j++) {
              if(!this.isEmpty(i,j)) {
                if ((i + 1 <= 3) && this.valueTable[i + 1][j] === this.valueTable[i][j]) {
                  this.valueTable[i + 1][j] = this.valueTable[i + 1][j] * 2;
                  this.valueTable[i][j] = 0;
                  console.log("fusion")
                  isDeplaced = true
                }
              }
            }
          }
          break;
    }
    if(isDeplaced)this.addCase(2)
    }.bind(this));

    for(let i = 0;i < this.nbrRow;i++){
      this.rowInTable.push(i);
      this.rowOfZero.push(0);
    }

    for(let j = 0;j < this.nbrRow;j++){
      this.valueTable.push([0,0,0,0])
    }

    this.addCase(2)
    this.addCase(2)
  },

  methods : {
    isEmpty : function (ligne,colonne){
      return this.valueTable[ligne][colonne] === 0
    },

    addCase: function (value){
      let randomColonne = Math.floor(Math.random() * this.nbrRow)
      let randomLigne = Math.floor(Math.random() * this.nbrRow)

      while(!this.isEmpty(randomColonne,randomLigne)){
        randomColonne = Math.floor(Math.random() * this.nbrRow)
        randomLigne = Math.floor(Math.random() * this.nbrRow)
      }

      this.valueTable[randomColonne][randomLigne] = value;
    },


  },
}
</script>

<style scoped>
  table {
    border-collapse: separate;
    border-spacing: 0.5rem;
    margin-left: auto;
    margin-right: auto;
    background-color: darkgray;
    border-radius: 5px;
  }
  td {
    width:5rem;
    height:5rem;
    margin: 1rem;
    background-color: gray;
    border-radius: 5px;
  }

  .two {
    background-color: #e1e1e1;
  }

  .four {
    background-color: #c9c91b;
  }

  .eight {
    background-color: orange;
  }

  .sixteen {
    background-color: #ef5a5a;
  }

  .thirtyTwo {
    background-color: red;
  }
</style>
