<template>
  <section>
    <h1 class="heading">Player List</h1>

  <a v-for="(player, idx) in playerData.players" :key="idx" :href="player.profilePageUrl">
    <div class="player-card" v-bind:style="{ 'background-image': 'url('+player.squadImage+')' }">
      <div class="card-content">
        <div class="card-header">
          <span> {{ player.firstName + " " + player.surname }} <span v-if="isNumeric(player.shirtNumber)">{{ " (" + player.shirtNumber + ")" }}</span> </span>
        </div>
        <div class="card-sub-header mrgbtm-5">
          {{ player.country }}
        </div>
        <div class="mrgbtm-5">
          <span >{{ player.position }}</span>
        </div>
        <div class="mrgbtm-5" v-if="player.joinDate">Joined: {{ date(player.joinDate) }}</div>
        <div v-else>Joined: Unknown</div>
        </div>
    </div>
  </a>
    

  </section>
</template>

<script>

import players from '../data/players.js'
import moment from 'moment'

export default {
  name: 'PlayerListing',
  methods: {
    moment: function (date) {
      return moment(date);
    },
    date: function (date) {
      return moment(date).format('DD/MM/YYYY');
    },
    isNumeric: function (n) {
      return !isNaN(parseInt(n)) && isFinite(n);
    }
  },
  data () {
    return {
      playerData: players
    }
  }
}
</script>

<style scoped>

  .heading {
    margin-left: 1rem;
    font-size: xx-large;
    padding: 1rem;
    color: white;
  }

  .heading, .card-content {
    background-image: linear-gradient(to left, rgba(255,0,0,0), rgb(86 6 20));
  }

  .player-card {
    position: relative;
    height: 25rem; 
    width: 25rem; 
    background-size: 25rem 25rem; 
    display: inline-block;
    margin: 1rem;
    border-radius: 5px;
    border: 10px solid;
    border-image-slice: 1;
    border-width: 5px;
    border-image-source: linear-gradient(to right, #5f1327, #b11f41);
  }
  .player-card:hover {
    box-shadow: 0px 0px 10px #fa91d4;
  }

  .card-content {
    padding: 1rem;
    position: absolute;
    bottom: 0px;
    color: white;
  }
  .card-header span {
    font-size: x-large;
    font-weight: bold;
  }

  .mrgbtm-5{
    margin-bottom: 5px;
  }
</style>
