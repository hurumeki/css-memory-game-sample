<template>
  <div>
    <input 
      v-for="c in cardCount" 
      :key="c" 
      :id="`check-${c}`"
      type="checkbox">

    <div class="cards">
      <div 
        v-for="c in cardCount"
        :key="c"
        :class="['card', `c-${c}`]">
        <label :for="`check-${c}`"/>
        <div class="front">
          <div class="face">
            {{ mark[c%markCount-1] }}
          </div>
        </div>
        <div class="back" />
      </div>    
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data: function() {
    return {
      mark: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
    }
  },
  computed: {
    markCount: function() {
      return this.mark.length
    },
    cardCount: function() {
      return this.markCount * 2
    }
  }
}
</script>

<style lang="scss">
$mark-count: 8;
$card-count: $mark-count * 2;

body {
  padding: 10px;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  width: calc((60px + 20px) * 4);
}

.card {
  border: 1px solid black;
  height: 100px;
  margin: 10px;
  text-align: center;
  transition: transform 1s;
  transform-style: preserve-3d;
  position: relative;
  width: 60px;

  label {
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
  }

  .front {
    background: white;
    transform: rotateY(180deg) translateZ(1px);
    position: absolute;
    height: 100%;
    width: 100%;

    .face {
      line-height: 100px;
    }
  }

  .back {
    background: black;
    position: absolute;
    height: 100%;
    width: 100%;
  }
}

@for $c from 1 through $card-count {
  #check-#{$c}:checked ~ .cards .card.c-#{$c} {
    transform: rotateY(180deg);

    label {
      transform: translateZ(-1px);
    }
  }
}
</style>
