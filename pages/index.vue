<template>
  <div>
    <input
      v-for="p in phaseCount"
      :key="p"
      :id="`radio-${p}`"
      :checked="p==1"
      :value="p"
      name="radio-phase"
      type="radio">
    <template
      v-for="p in phaseCount">
      <input
        v-for="c in cardCount"
        :key="p,c"
        :id="`radio-${p}-check-${c}`"
        type="checkbox">
      <input
        v-for="c in cardCount"
        :key="p,c"
        :id="`radio-${p}-check-${c}-wrong`"
        :class="[`p-${p}`]"
        type="checkbox">
    </template>

    <div class="cards">
      <div
        v-for="c in cardCount"
        :key="c"
        :class="['card', `c-${c}`]">
        <label
          v-for="p in phaseCount"
          :key="p,c"
          :for="`radio-${p}-check-${c}`"
          :class="['open', `p-${p}`]"/>
        <label
          v-for="p in phaseCount"
          :key="p,c"
          :for="`radio-${p}-check-${c}-wrong`"
          :class="['wrong', `m-${(c-1)%markCount + 1}`, `p-${p}`]"/>
        <div class="front">
          <div class="face">
            {{ mark[(c-1)%markCount] }}
          </div>
        </div>
        <div class="back" />
      </div>
    </div>

    <div class="failed">
      <label for="radio-2"/>
      お手付き
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data: function() {
    return {
      phaseCount: 3,
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
$phase-count: 3;
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
    display: none;
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

.failed {
  display: none;
  position: relative;
  width: 300px;
  height: 100px;

  label {
    position: absolute;
    width: 100%;
    height: 100%;
    display: block;
  }
}

.card-rotate {
  transform: rotateY(180deg);
  label {
    transform: translateZ(-1px);
  }
}

.show {
  display: block;
}

@for $p from 1 through $phase-count {
  #radio-#{$p}:checked ~ .cards .card .p-#{$p}.open {
    @extend .show;
  }

  @for $c from 1 through $card-count {
    #radio-#{$p}:checked
      ~ #radio-#{$p}-check-#{$c}:checked
      ~ .cards
      .card.c-#{$c} {
      @extend .card-rotate;
    }

    #radio-#{$p}:checked
      ~ #radio-#{$p}-check-#{$c}-wrong:checked
      ~ .cards
      .card.c-#{$c} {
      @extend .card-rotate;
    }

    #radio-#{$p}:checked
      ~ #radio-#{$p}-check-#{$c}:checked
      ~ .cards
      .card:not(.c-#{$c})
      :not(.m-#{($c - 1)%$mark-count + 1}).p-#{$p}.wrong {
      @extend .show;
    }
  }

  #radio-#{$p}:checked ~ [id$='wrong'].p-#{$p}:checked ~ .failed {
    @extend .show;
  }
}
</style>
