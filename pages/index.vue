<template>
  <div>
    <input
      id="check"
      type="checkbox">
    <div class="card">
      <label for="check"/>
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

:checked + .card {
  transform: rotateY(180deg);

  label {
    transform: translateZ(-1px);
  }
}
</style>
