<template>
  <form @submit.prevent>
    <div class="inputs">
      <fieldset>
        <legend>name</legend>
        <my-input v-model="organization.name" type="text" />
      </fieldset>
      <fieldset>
        <legend>coordinates</legend>
        <div>
          <legend>x</legend>
          <my-input
            v-model="organization.coordinates.x"
            type="number"
            max="5"
            min="-5"
          />
          <legend>y</legend>
          <my-input
            v-model="organization.coordinates.y"
            type="number"
            max="5"
            min="-5"
          />
        </div>
      </fieldset>
      <fieldset>
        <legend>annualTurnover</legend>
        <my-input
          v-model="organization.annualTurnover"
          type="number"
          max="5"
          min="-5"
        />
      </fieldset>
      <fieldset>
        <legend>type</legend>
        <my-select v-model="organization.type" :options="typeOptions" />
      </fieldset>
      <fieldset>
        <legend>officialAddress</legend>
        <my-input v-model="organization.officialAddress.zipCode" type="text" />
      </fieldset>
    </div>
    <div class="commandButton">
      <my-button type="button" @click="create">отправить</my-button>
    </div>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import axios from "axios";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: { MySelect, MyInput, MyButton },
  props: {
    organizationProp: Object,
  },
  watch: {
    organizationProp: {
      handler(newOrganization) {
        this.organization = JSON.parse(JSON.stringify(newOrganization));
      },
    },
  },
  data() {
    return {
      organization: JSON.parse(JSON.stringify(this.organizationProp)),
      typeOptions: [
        { value: "PUBLIC", name: "PUBLIC" },
        { value: "GOVERNMENT", name: "GOVERNMENT" },
        { value: "TRUST", name: "TRUST" },
        { value: "PRIVATE_LIMITED_COMPANY", name: "PRIVATE_LIMITED_COMPANY" },
        { value: "OPEN_JOINT_STOCK_COMPANY", name: "OPEN_JOINT_STOCK_COMPANY" },
      ],
    };
  },
  methods: {
    create() {
      axios
        .put(
          "https://localhost:8181/organization-service/organizations/" +
            this.organization.id,
          {
            name: this.organization.name,
            coordinates: this.organization.coordinates,
            type: this.organization.type,
            annualTurnover: this.organization.annualTurnover,
            officialAddress: this.organization.officialAddress,
          }
        )
        .then(() => {
          this.$emit("closeMoreInfo");
          window.location.reload();
        });
    },
  },
};
</script>

<style scoped>
fieldset {
  margin-top: 5px;
  padding: 5px;
}

.commandButton {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.inputs {
  height: 100%;
}

.button {
  width: 150px;
  font-size: 15px;
}
</style>
