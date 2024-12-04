<template>
  <div class="dotTableRow">
    <div class="dotRowElem dotRowNormalElem"> column </div>
    <div class="dotRowElem dotRowNormalElem"> type </div>
    <div class="dotRowElem dotRowShortElem"></div>
  </div>
</template>

<style scoped>
.dotTableRow {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  color: white;
  text-align: center;
}

.dotRowShortElem {
  width: 5%;
}

.dotRowNormalElem {
  width: 25%;
}

.dotRowLongElem {
  width: 30%;
}
</style>
