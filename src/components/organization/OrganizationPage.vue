<template>
  <div v-show="element !== 'form' && element !== 'update'" class="page">
    <div v-show="element === 'table'" class="organizationTable">
      <organizations-block
        ref="organizations"
        :headerOrganization="headerOrganization"
        @moreInfo="moreInfo"
        @updateOrganization="updateOrganization"
        @reload="reload"
      ></organizations-block>
    </div>
    <div v-show="element === 'info'" class="elem">
      <my-button
        class="closeButton"
        type="button"
        @click="closeMoreInfo"
        @reload="reload"
        >x
      </my-button>
      <div class="header">
        <h2>Информация об огранизации</h2>
      </div>
      <organization-info
        :headerOrganization="headerOrganization"
        :organization-prop="currentOrganization"
      />
    </div>
    <my-button class="my-button" type="button" @click="addOrganization">
      Добавить организацию
    </my-button>
    <util-block @moreInfo="moreInfo" @reload="reload"></util-block>
  </div>
  <div v-show="element === 'form'" class="elem">
    <my-button class="closeButton" type="button" @click="closeMoreInfo"
      >x
    </my-button>
    <div class="header">
      <h2>Добавить организацию</h2>
    </div>
    <organization-form @closeMoreInfo="closeMoreInfo" @reload="reload" />
  </div>
  <div v-show="element === 'update'" class="elem">
    <my-button
      class="closeButton"
      type="button"
      @click="closeMoreInfo"
      @reload="reload"
      >x
    </my-button>
    <div class="header">
      <h2>Изменить организацию</h2>
    </div>
    <organization-update-form
      :organizationProp="currentOrganization"
      @closeMoreInfo="closeMoreInfo"
      @reload="reload"
    />
  </div>
</template>

<script>
import OrganizationInfo from "@/components/organization/OrganizationInfo.vue";
import MyButton from "@/components/UI/MyButton.vue";
import OrganizationForm from "@/components/organization/OrganizationForm.vue";
import OrganizationsBlock from "@/components/organization/OrganizationsBlock.vue";
import OrganizationUpdateForm from "@/components/organization/OrganizationUpdateForm.vue";
import MyInput from "@/components/UI/MyInput.vue";
import MySelect from "@/components/UI/MySelect.vue";
import UtilBlock from "@/components/UtilBlock.vue";
import SortingTableRow from "@/components/sort/SortingTableRow.vue";

export default {
  components: {
    SortingTableRow,
    UtilBlock,
    MySelect,
    MyInput,
    OrganizationUpdateForm,
    OrganizationsBlock,
    OrganizationForm,
    MyButton,
    OrganizationInfo,
  },
  data() {
    return {
      type: "",
      typeOptions: [
        { value: "PUBLIC", name: "PUBLIC" },
        { value: "GOVERNMENT", name: "GOVERNMENT" },
        { value: "TRUST", name: "TRUST" },
        { value: "PRIVATE_LIMITED_COMPANY", name: "PRIVATE_LIMITED_COMPANY" },
        { value: "OPEN_JOINT_STOCK_COMPANY", name: "OPEN_JOINT_STOCK_COMPANY" },
      ],
      element: "table",
      headerOrganization: {
        id: "id",
        name: "Имя",
        coordinates: "Координаты",
        creationDate: "Дата создания",
        type: "Тип",
        officialAddress: "Официальный адресс",
        annualTurnover: "Годовой оборот",
      },
      currentOrganization: {
        name: "",
        coordinates: {
          x: 0,
          y: 0,
        },
        annualTurnover: "",
        type: "",
        officialAddress: {
          zipCode: "",
        },
        employees: [],
      },
    };
  },
  methods: {
    moreInfo(organization) {
      this.currentOrganization = organization;
      this.element = "info";
    },
    updateOrganization(organization) {
      this.currentOrganization = organization;
      this.element = "update";
    },
    closeMoreInfo() {
      this.element = "table";
      this.reload();
    },
    addOrganization() {
      this.element = "form";
    },
    reload() {
      this.$refs.organizations.getOrganizations();
    },
  },
};
</script>

<style scoped>
.page {
  width: 1300px;
  height: 650px;
}

.organizationTable {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

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

.elem {
  height: 100%;
  width: 100%;
  flex-direction: column;
  overflow-y: scroll;
  position: relative;
  border: black solid 1.5px;
  padding: 10px;
}

.dotTableHeader {
  background-color: #828670;
  border: 1.5px solid black;
  padding: 10px 0px 10px 0px;
  margin-bottom: 10px;
}

.dotTableHeader :deep(div) {
  background-color: #828670;
  color: black;
}

.closeButton {
  margin: 5px;
  padding: 0;
  width: 20px;
  height: 20px;
  position: absolute;
  top: 0;
  right: 0;
}

.util-button {
  width: 300px;
  height: 30px;
  margin: 5px;
}

.header {
  padding: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.my-button {
  width: 100%;
}

.text {
  width: 400px;
  height: 30px;
  border: 1.5px solid black;
  padding: 8px;
}
</style>
