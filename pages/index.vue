<template>
  <div>
    <input
      id="check"
      type="checkbox">
    <div class="card">
      <div class="front">
        <div class="face">
          Card
        </div>
      </div>
      <div class="back" />
    </div>    
  </div>
</template>

<style lang="scss">
body {
  padding: 10px;
}

.card {
  border: 1px solid black;
  height: 100px;
  text-align: center;
  transition: transform 1s;
  transform-style: preserve-3d;
  position: relative;
  width: 60px;

  .front {
    background: white;
    transform: rotateY(180deg);
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

:checked + .card {
  transform: rotateY(180deg);
}
</style>
