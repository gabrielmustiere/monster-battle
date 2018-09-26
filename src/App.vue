<template>
  <div class="container">
    <div class="row">
      <div
        :style="{ paddingTop: '30px' }"
        class="col-md-12">
        <div class="text-center jumbotron">
          <h1>La bagarre !</h1>
        </div>
      </div>
    </div>

    <div class="row justify-content-center">
      <div class="col-4">
        <div class="text-center">
          <h2>{{ player.name }}</h2>
        </div>
        <div class="progress">
          <div
            :style="{width : player.currentLife + '%'}"
            :aria-valuenow="player.currentLife"
            :aria-valuemin="minLife"
            :aria-valuemax="maxLife"
            class="progress-bar bg-success"
            role="progressbar">
            {{ player.currentLife }}
          </div>
        </div>
      </div>

      <div class="col-4">
        <div class="text-center">
          <h2>{{ monster.name }}</h2>
        </div>
        <div class="progress">
          <div
            :style="{width : monster.currentLife + '%'}"
            :aria-valuenow="monster.currentLife"
            :aria-valuemin="minLife"
            :aria-valuemax="maxLife"
            class="progress-bar bg-success"
            role="progressbar">
            {{ monster.currentLife }}
          </div>
        </div>
      </div>
    </div>

    <div
      v-show="!isBattle"
      :style="{ paddingTop: '30px' }"
      class="row">
      <div class="col">
        <div class="card">
          <div class="card-body text-center">
            <button
              class="btn btn-lg btn-info"
              @click="beginBattle()">Commencer la partie</button>
          </div>
        </div>
      </div>
    </div>

    <div
      v-show="isBattle"
      :style="{ paddingTop: '30px' }"
      class="row">
      <div class="col">
        <div class="card">
          <div class="card-body text-center">
            <button
              class="btn btn-lg btn-danger mx-3"
              @click="attack()">Attaquer</button>
            <button
              class="btn btn-lg btn-warning mx-3" 
              @click="specialAttack()">Attaque spécial</button>
            <button
              class="btn btn-lg btn-success mx-3"
              @click="heal()">Soin</button>
            <button
              class="btn btn-lg btn-light mx-3"
              @click="giveUpBattle()">Fuir</button>
          </div>
        </div>
      </div>
    </div>

    <div
      v-show="isBattle"
      :style="{ paddingTop: '30px' }"
      class="row">
      <div class="col">
        <div class="card">
          <div class="card-body text-center">
            <ul class="list-unstyled">
              <li
                v-for="(turn,i) in turns"
                :key="i">{{ turn.character.name }} {{ turn.actionType.toLowerCase() }} {{ turn.opponent.name }} pour {{ turn.value }}
              </li>
            </ul>

          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
const ATTAQUE = "ATTAQUE";
const HEAL = "HEAL ";
const SPECIAL_ATTAQUE = "ATTAQUE SPéCIALE";
export default {
  data: function () {
    return {
      isBattle: false,
      maxLife: 100,
      minLife: 0,
      player: {
        name: "Gabriel",
        currentLife: 0
      },
      monster: {
        name: "Monstre",
        currentLife: 0
      },
      currentCharacter: null,
      turns: []
    }


  },
  methods: {
    beginBattle: function () {
      this.player.currentLife = 100;
      this.monster.currentLife = 100;
      this.currentCharacter = this.player;
      this.isBattle = true
    },
    giveUpBattle: function () {
      this.player.currentLife = 0;
      this.monster.currentLife = 0;
      this.isBattle = false;
      this.currentCharacter = this.player;
      this.turns = []
    },
    getRandomValue () {
      return Math.floor(Math.random() * Math.floor(20))
    },
    getRandomAttackValue () {
      return this.getRandomValue()
    },
    getRandomAttackSpecialValue () {
      return Math.round(this.getRandomAttackValue() * 1.5)
    },
    getHealValue () {
      return Math.round(this.getRandomValue() * 0.8)
    },

    attack () {
      let turn = this.getTurnElement(
        this.currentCharacter,
        this.getOpponent(this.currentCharacter),
        ATTAQUE,
        this.getRandomAttackValue()
      );
      this.applyTurn(turn);
      this.logTurn(turn);
      this.switchCharacter()
    },

    specialAttack () {
      let turn = this.getTurnElement(
        this.currentCharacter,
        this.getOpponent(this.currentCharacter),
        SPECIAL_ATTAQUE,
        this.getRandomAttackSpecialValue()
      );
      this.applyTurn(turn);
      this.logTurn(turn);
      this.switchCharacter()
    },
    heal () {
      let turn = this.getTurnElement(this.currentCharacter, this.currentCharacter, HEAL, this.getHealValue());
      this.applyTurn(turn);
      this.logTurn(turn);
      this.switchCharacter()
    },

    switchCharacter () {
      if (this.currentCharacter === this.player) {
        this.currentCharacter = this.monster
        //TODO RANDOM ACTION
      } else {
        this.currentCharacter = this.player
      }
    },

    getOpponent () {
      if (this.currentCharacter === this.player) {
        return this.monster
      }
      return this.player
    },

    getTurnElement (character, opponent, actionType, value) {
      return {
        character: character,
        opponent: opponent,
        actionType: actionType,
        value: value
      }
    },
    applyTurn (turn) {
      switch (turn.actionType) {
        case ATTAQUE:
        case SPECIAL_ATTAQUE: {
          turn.opponent.currentLife -= turn.value;
          break
        }
        case HEAL:
          turn.character.currentLife += turn.value;
          break
      }
    },
    logTurn (turn) {
      this.turns.unshift(turn)
    }
  }
}
</script>

<style scoped></style>
