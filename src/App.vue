<template>
  <div class="tic-tac-toe">
    <h1>Tris</h1>
    <div class="tabellone">
      <div v-for="(riga, indiceRiga) in tabellone" :key="indiceRiga" class="riga">
        <div v-for="(cella, indiceCella) in riga" :key="indiceCella" class="cella" @click="gestisciClick(indiceRiga, indiceCella)">
          {{ cella }}
        </div>
      </div>
    </div>
    <div v-if="vincitore" class="risultato">
      <p>{{ vincitore }} ha vinto!</p>
      <button @click="reinizializzaGioco">Gioca di nuovo</button>
    </div>
    <div v-if="pareggio && !vincitore" class="risultato">
      <p>Pareggio!</p>
      <button @click="reinizializzaGioco">Gioca di nuovo</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      giocatoreCorrente: 'X',
      tabellone: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ],
      vincitore: null,
      pareggio: false
    }
  },
  methods: {
    gestisciClick(riga, colonna) {
      if (this.tabellone[riga][colonna] !== '') {
        return;
      }
      this.tabellone[riga][colonna] = this.giocatoreCorrente;
      if (this.controllaVincitore()) {
        this.vincitore = this.giocatoreCorrente;
      } else if (this.controllaPareggio()) {
        this.pareggio = true;
      } else {
        this.giocatoreCorrente = this.giocatoreCorrente === 'X' ? 'O' : 'X';
      }
    },
    controllaVincitore() {
      // Controllo righe
      for (let i = 0; i < 3; i++) {
        if (this.tabellone[i][0] !== '' && this.tabellone[i][0] === this.tabellone[i][1] && this.tabellone[i][1] === this.tabellone[i][2]) {
          return true;
        }
      }
      // Controllo colonne
      for (let i = 0; i < 3; i++) {
        if (this.tabellone[0][i] !== '' && this.tabellone[0][i] === this.tabellone[1][i] && this.tabellone[1][i] === this.tabellone[2][i]) {
          return true;
        }
      }
      // Controllo diagonali
      if (this.tabellone[0][0] !== '' && this.tabellone[0][0] === this.tabellone[1][1] && this.tabellone[1][1] === this.tabellone[2][2]) {
        return true;
      }
      if (this.tabellone[2][0] !== '' && this.tabellone[2][0] === this.tabellone[1][1] && this.tabellone[1][1] === this.tabellone[0][2]) {
return true;
}
return false;
},
controllaPareggio() {
for (let riga = 0; riga < 3; riga++) {
for (let colonna = 0; colonna < 3; colonna++) {
if (this.tabellone[riga][colonna] === '') {
return false;
}
}
}
return true;
},
reinizializzaGioco() {
this.giocatoreCorrente = 'X';
this.tabellone = [
['', '', ''],
['', '', ''],
['', '', '']
];
this.vincitore = null;
this.pareggio = false;
}
}
}
</script>


<style>
  .tic-tac-toe {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

  .tabellone {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 300px;
    height: 300px;
    border: 2px solid #333;
    border-radius: 10px;
    background-color: #eee;
  }

  .riga {
    display: flex;
  }

  .cella {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    font-size: 4rem;
    cursor: pointer;
    border: 2px solid #333;
  }

  .cella:hover {
    background-color: #ddd;
  }

  .risultato {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    background-color: rgba(0, 0, 0, 0.5);
    font-size: 4rem;
    color: #fff;
  }

  .risultato button {
    margin-top: 2rem;
    padding: 1rem;
    background-color: #333;
    color: #fff;
    font-size: 2rem;
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  .risultato button:hover {
    background-color: #555;
  }
</style>
