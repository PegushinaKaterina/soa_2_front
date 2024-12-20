<template>
  <div class="dotTable">
    <div class="dotTableRow">
      <div class="dotRowElem">
        {{ headerOrganization.name }}
      </div>
      <div class="dotRowElem">
        {{ headerOrganization.coordinates }}
      </div>
      <div class="dotRowElem">
        {{ headerOrganization.creationDate }}
      </div>
      <div class="dotRowElem">
        {{ headerOrganization.type }}
      </div>
      <div class="dotRowElem">
        {{ headerOrganization.annualTurnover }}
      </div>
      <div class="dotRowElem">
        {{ headerOrganization.officialAddress }}
      </div>
    </div>
    <div class="dotTableRow">
      <div class="dotRowElem">{{ organization.name }}</div>
      <div class="dotRowElem">
        x: {{ organization.coordinates.x }}, y: {{ organization.coordinates.x }}
      </div>
      <div class="dotRowElem">
        {{ new Date(organization.creationDate).toLocaleDateString() }}
      </div>
      <div class="dotRowElem">
        {{ organization.type }}
      </div>
      <div class="dotRowElem">
        {{ organization.annualTurnover }}
      </div>
      <div class="dotRowElem">
        {{ organization.officialAddress.zipCode }}
      </div>
    </div>
    <div class="dotRowElem column employees">
      Всего сотрудников в огранизации: {{ organization.employees.length }}
      <div v-for="employee in organization.employees">
        {{ employee.name }}
      </div>
    </div>
  </div>
  <div class="row">
    <my-button class="closeButton" type="button" @click="deleteAllEmployees"
      >удалить всех сотрудников
    </my-button>
    <div>
      <fieldset class="my-input">
        <legend>name</legend>
        <my-input v-model="name" type="text"/>
      </fieldset>
      <my-button class="closeButton" type="button" @click="addEmployee"
        >Добавить сотрудника
      </my-button>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MyInput from "@/components/UI/MyInput.vue";

export default {
  name: "organization-info",
  components: { MyInput, MyButton },
  props: {
    organizationProp: {
      type: Object,
      required: true,
    },
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
      name: "",
      headerOrganization: {
        id: "id",
        name: "Имя",
        coordinates: "Координаты",
        creationDate: "Дата создания",
        type: "Тип",
        officialAddress: "Официальный адресс",
        annualTurnover: "Годовой оборот",
        employees: "Сотрудники",
      },
    };
  },
  mounted() {
    this.getOrganization();
  },
  methods: {
    getOrganization() {
      if (this.organizationProp && this.organizationProp.id) {
        axios
          .get(
            "https://localhost:8181/organization-service/organizations/" +
              this.organization.id
          )
          .then((res) => {
            this.organization = res.data;
          })
          .catch((error) => alert(error));
      }
    },
    deleteAllEmployees() {
      axios
        .post(
          "https://localhost:8585/orgmanager/fire/all/" + this.organization.id
        )
        .then(() => {
          this.getOrganization();
        })
        .catch((error) => alert(error));
    },
    addEmployee() {
      if (this.name === "") {
        alert("Имя сотрудника не может быть пустым");
      }
      axios
        .post(
          "https://localhost:8585/orgmanager/hire/" + this.organization.id,
          {
            name: this.name,
          }
        )
        .then(() => {
          this.getOrganization();
        })
        .catch((error) => alert(error));
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

.dotTableRow {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: start;
  color: white;
  text-align: center;
  padding: 0px 20px;
}

.dotTable {
  height: 480px;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: start;
  color: white;
  text-align: center;
  padding: 5px;
  overflow-y: scroll;
}

.dotRowElem {
  display: flex;
  flex-direction: row;
  padding: 2px;
}

.my-input {
  padding: 5px;
}

.column {
  display: flex;
  flex-direction: column;
  justify-content: start;
}

.employees {
  overflow-y: scroll;
  border: #828670 1px solid;
}
</style>
