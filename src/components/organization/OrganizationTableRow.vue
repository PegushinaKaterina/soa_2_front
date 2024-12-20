<template>
  <div class="dotTableRow">
    <div
      class="dotRowElem dotRowNormalElem"
      @click="$emit('moreInfo', organization)"
    >
      {{ organization.name }}
    </div>
    <div
      class="dotRowElem dotRowNormalElem"
      @click="$emit('moreInfo', organization)"
    >
      x: {{ organization.coordinates.x }}, y: {{ organization.coordinates.x }}
    </div>
    <div
      class="dotRowElem dotRowLongElem"
      @click="$emit('moreInfo', organization)"
    >
      {{ new Date(organization.creationDate * 1000).toLocaleDateString() }}
    </div>
    <div
      class="dotRowElem dotRowNormalElem"
      @click="$emit('moreInfo', organization)"
    >
      {{ organization.type }}
    </div>
    <div
      class="dotRowElem dotRowNormalElem"
      @click="$emit('moreInfo', organization)"
    >
      {{ organization.annualTurnover }}
    </div>
    <div
      class="dotRowElem dotRowNormalElem"
      @click="$emit('moreInfo', organization)"
    >
      {{ organization.officialAddress.zipCode }}
    </div>
    <div class="dotRowElem dotRowShortElem">
      <my-button
        class="closeButton"
        type="button"
        @click="$emit('updateOrganization', organization)"
        >✏️
      </my-button>
    </div>
    <div class="dotRowElem dotRowShortElem">
      <my-button class="closeButton" type="button" @click="deleteOrganization"
        >x
      </my-button>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";

export default {
  name: "organization-table-row",
  components: { MyButton },
  props: {
    organization: {
      type: Object,
      required: true,
    },
  },
  methods: {
    moreInfo() {
      this.$emit("moreInfo", this.organization);
    },
    deleteOrganization() {
      axios
        .delete(
          "https://localhost:8181/organization-service/organizations/" +
            this.organization.id
        )
        .then(() => this.$emit("reload"))
        .catch((error) => alert(error));
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
  padding: 10px;
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

.closeButton {
  margin: 0;
  padding: 0;
  width: 20px;
  height: 20px;
  border-radius: 5px;
}

.dotTableRow:has(.dotRowElem:hover) {
  background-color: wheat;
}

.dotTableRow:has(.dotRowElem:hover) :deep(.dotRowElem) {
  background-color: wheat;
}
</style>
