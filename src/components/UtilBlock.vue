<template>
  <div class="row" style="margin-top: 10px">
    <my-button
      class="util-button"
      style=""
      type="button"
      @click="minOrganization"
    >
      Организация с минимальным типом
    </my-button>
    <div class="row">
      <div class="column">
        <my-input
          v-model="officialAddress"
          class="util-button"
          type="text"
          @focus="changeAddress"
        />
        <my-select
          v-model="type"
          :options="typeOptions"
          class="util-button"
          style="height: 30px"
          @change="changeType"
        />
      </div>
      <div class="column">
        <div class="row">
          <div class="text util-button">
            Количество организаций с заданным адресом:
            {{ minOrganizationCount }}
          </div>
          <my-button type="button" @click="countOrganization">
            Показать
          </my-button>
        </div>
        <div class="row">
          <div class="text util-button">
            Удалено организаций: {{ deleteOrganizationCount }}
          </div>
          <my-button type="button" @click="deleteOrganization">
            Удалить
          </my-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MySelect from "@/components/UI/MySelect.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MyInput from "@/components/UI/MyInput.vue";

export default {
  components: {
    MyInput,
    MySelect,
    MyButton,
  },
  data() {
    return {
      type: "",
      officialAddress: "",
      typeOptions: [
        { value: "PUBLIC", name: "PUBLIC" },
        { value: "GOVERNMENT", name: "GOVERNMENT" },
        { value: "TRUST", name: "TRUST" },
        { value: "PRIVATE_LIMITED_COMPANY", name: "PRIVATE_LIMITED_COMPANY" },
        { value: "OPEN_JOINT_STOCK_COMPANY", name: "OPEN_JOINT_STOCK_COMPANY" },
      ],
      deleteOrganizationCount: null,
      minOrganizationCount: null,
    };
  },
  methods: {
    changeType() {
      this.deleteOrganizationCount = null;
    },
    changeAddress() {
      this.minOrganizationCount = null;
    },
    minOrganization() {
      axios
        .get(
          "https://localhost:8181/organization-service/organizations/min/type"
        )
        .then((res) => {
          this.$emit("moreInfo", res.data);
        })
        .catch((error) => alert(error));
    },
    countOrganization() {
      if (this.officialAddress === "") {
        alert("Адресс организации не может быть пустым");
      } else if (this.officialAddress.length >= 18) {
        alert("Адресс организации должен быть не больше 18 символов");
      } else {
        axios
          .get(
            "https://localhost:8181/organization-service/organizations/count/official-address/" +
              this.officialAddress
          )
          .then((res) => {
            this.minOrganizationCount = res.data.count;
          })
          .catch((error) => alert(error));
      }
    },
    deleteOrganization() {
      if (this.type === "") {
        alert("Тип организации не может быть пустым");
      } else {
        axios
          .delete(
            "https://localhost:8181/organization-service/organizations/type/" +
              this.type
          )
          .then((res) => {
            this.$emit("reload");
            this.deleteOrganizationCount = res.data.count;
          })
          .catch((error) => alert(error));
      }
    },
  },
};
</script>

<style scoped>
.row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.column {
  display: flex;
  flex-direction: column;
  justify-content: start;
}

.util-button {
  width: 300px;
  height: 30px;
  margin: 5px;
}

.text {
  width: 400px;
  height: 30px;
  padding: 8px;
}
</style>
