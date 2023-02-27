<template>
  <main id="container">
    <div>
      <h1>Qu<span>ant</span>u<span>man</span>ia</h1>
      <div class="btn-group">
        <button @click="goAnt">Move</button>
      </div>
      <div id="tiles">
        <div
          v-for="tiles in grids"
          :ref="
            (el) => {
              grids[tiles] = el;
            }
          "
          :key="tiles"
        >
          <div
            v-for="tile in tiles"
            class="tile"
            :ref="
              (el) => {
                tiles[tile] = el;
              }
            "
            :id="tile"
            :key="tile"
          >
            <img class="d-none" src="./assets/222.png" alt="Ant image" />
          </div>
        </div>
      </div>
    </div>
    <div id="content">
      <p>
        <a
          href="https://en.wikipedia.org/wiki/Langton%27s_ant"
          target="_blank"
          title="Langton's ant"
          >Langton's ant</a
        >
      </p>
      <canvas id="grid-canvas" width="400" height="400" />
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { goAnt } from "./composables/quantumania";
import { ant } from "./composables/ant";

const grids = ref([]);

const makeGridArray = (cols, rows) => {
  let arr = new Array(cols);
  for (let i = 0; i < arr.length; i++) {
    arr[i] = new Array(rows);
    for (let j = 0; j < arr[i].length; j++) {
      arr[i][j] = `${i},${j}`;
    }
  }
  return arr;
};

grids.value = makeGridArray(10, 10);

onMounted(() => {
  // goAnt();
  ant();
});
</script>

<style>
body,
html {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-color: rgb(235, 228, 219);
}

h1 {
  display: block;
  width: 90%;
  text-align: center;
  color: lime;
  background-image: linear-gradient(
    -225deg,
    #231557 0%,
    #44107a 29%,
    #ff1361 67%,
    #fff800 100%
  );
  padding: 2rem;
  margin-bottom: 0;
  font-size: 2rem;
}

span {
  color: rgb(25, 5, 79);
  font-size: xx-large;
}

.btn-group {
  display: flex;
  justify-content: start;
  padding: 2rem;
}

.btn-group > button {
  padding: 0.4rem 0.8rem;
  font-size: large;
  border: rgb(204, 118, 12) 2px solid;
  border-radius: 10%;
  cursor: pointer;
}

#container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  padding: 1rem;
  height: 100%;
}

#content {
  width: 400px;
  margin-top: 2rem;
}

#grid-canvas {
  border: 2px solid rgb(224, 108, 58);
  display: block;
  background: white;
}

#tiles {
  margin: 0;
  padding: 0%;
  display: grid;
  grid-template-columns: repeat(10, 80px);
  grid-template-rows: repeat(10, 80px);
  /* margin-top: 2rem; */
  background-image: linear-gradient(to top, #e6e9f0 0%, #eef1f5 100%);
}

.visited {
  background-image: linear-gradient(
    -225deg,
    #231557 0%,
    #44107a 29%,
    #ff1361 67%,
    #fff800 100%
  );
}

img {
  width: 25px;
}

.d-none {
  display: none;
}

.tile {
  width: 80px;
  height: 80px;
  outline: 1px solid #000;
  display: flex;
  align-items: center;
  justify-content: center;
}

.rotate-90 {
  transform: rotate(90deg);
  -moz-transform: rotate(90deg);
  -webkit-transform: rotate(90deg);
}

.rotate--90 {
  transform: rotate(-90deg);
  -moz-transform: rotate(-90deg);
  -webkit-transform: rotate(-90deg);
}

.rotate-180 {
  transform: rotate(-180deg);
  -moz-transform: rotate(-180deg);
  -webkit-transform: rotate(-180deg);
}
</style>
