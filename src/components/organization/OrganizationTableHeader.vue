<template>
  <div class="dotTableRow">
    <div class="dotRowElem dotRowNormalElem">{{ organization.name }}</div>
    <div class="dotRowElem dotRowNormalElem">{{ organization.coordinates }}</div>
    <div class="dotRowElem dotRowLongElem">
      {{ organization.creationDate }}
    </div>
    <div class="dotRowElem dotRowShortElem">{{ organization.type }}</div>
    <div class="dotRowElem dotRowNormalElem">
      {{ organization.annualTurnover }}
    </div>
    <div class="dotRowElem dotRowNormalElem">
      {{ organization.officialAddress }}
    </div>
    <div class="dotRowElem dotRowShortElem"></div>
    <div class="dotRowElem dotRowShortElem"></div>
  </div>
</template>

<script>
export default {
  props: {
    organization: {
      type: Object,
      required: true,
    },
  },
};
</script>

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
