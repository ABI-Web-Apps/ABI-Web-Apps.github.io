<template>
  <div class="main">
    <div class="up">
      <button class="card1" @click="() => handleCardClick('heart')">
        Heart
      </button>
      <button class="card2" @click="() => handleCardClick('stomach')">
        Stomach
      </button>
    </div>
    <div class="down">
      <button class="card3" @click="() => handleCardClick('breast')">
        Breast
      </button>
      <button class="card4" @click="() => handleCardClick('lungs')">
        Lungs
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
const handleCardClick = (name: string) => {
  if (name == "heart") {
    window.open("https://copper3d-brids.github.io/my_heart/", "_blank");
  } else if (name == "stomach") {
    // window.open("https://sparc.science/datasets/136?type=dataset", "_blank");
  } else if (name == "lungs") {
    window.open("http://sites.bioeng.auckland.ac.nz/medtech/lungs", "_blank");
  } else if (name == "breast") {
    window.open(
      "https://abi-ctt-group.github.io/breast-educational-resource/model-breast/",
      "_blank"
    );
  }
};
</script>

<style scoped>
/* From Uiverse.io by Praashoo7 */
.main {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
}

.up {
  display: flex;
  flex-direction: row;
  gap: 1px;
}

.down {
  display: flex;
  flex-direction: row;
  gap: 1px;
}

.card1 {
  width: 90px;
  height: 90px;
  outline: none;
  border: none;
  background: white;
  border-radius: 90px 5px 5px 5px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  transition: 0.2s ease-in-out;
}

.instagram {
  margin-top: 1.5em;
  margin-left: 1.2em;
  fill: #cc39a4;
}

.card2 {
  width: 90px;
  height: 90px;
  outline: none;
  border: none;
  background: white;
  border-radius: 5px 90px 5px 5px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  transition: 0.2s ease-in-out;
}

.twitter {
  margin-top: 1.5em;
  margin-left: -0.9em;
  fill: #03a9f4;
}

.card3 {
  width: 90px;
  height: 90px;
  outline: none;
  border: none;
  background: white;
  border-radius: 5px 5px 5px 90px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  transition: 0.2s ease-in-out;
}

.github {
  margin-top: -0.6em;
  margin-left: 1.2em;
}

.card4 {
  width: 90px;
  height: 90px;
  outline: none;
  border: none;
  background: white;
  border-radius: 5px 5px 90px 5px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  transition: 0.2s ease-in-out;
}

.discord {
  margin-top: -0.9em;
  margin-left: -1.2em;
  fill: #8c9eff;
}

.card1:hover {
  cursor: pointer;
  scale: 1.1;
  background-color: #cc39a4;
}

.card1:hover .instagram {
  fill: white;
}

.card2:hover {
  cursor: pointer;
  scale: 1.1;
  background-color: #03a9f4;
}

.card2:hover .twitter {
  fill: white;
}

.card3:hover {
  cursor: pointer;
  scale: 1.1;
  background-color: pink;
}

.card3:hover .github {
  fill: white;
}

.card4:hover {
  cursor: pointer;
  scale: 1.1;
  background-color: #8c9eff;
}

.card4:hover .discord {
  fill: white;
}
</style>
