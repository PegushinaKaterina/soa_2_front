<template>
  <div v-show="element !== 'form' && element !== 'update'" class="page">
    <div v-show="element === 'table'" class="organizationTable">
      <organizations-block
        :headerOrganization="headerOrganization"
        @moreInfo="moreInfo"
        @updateOrganization="updateOrganization"
      ></organizations-block>
    </div>
    <div v-show="element === 'info'" class="elem">
      <my-button class="closeButton" type="button" @click="closeMoreInfo"
        >x</my-button
      >
      <div class="header">
        <h2>Информация об огранизации</h2>
      </div>
      <organization-info
        :headerOrganization="headerOrganization"
        :organization-prop="currentOrganization"
      />
    </div>
    <my-button type="button" @click="addOrganization" class="my-button">
      Добавить организацию
    </my-button>
  </div>
  <div v-show="element === 'form'" class="elem">
    <my-button class="closeButton" type="button" @click="closeMoreInfo"
      >x</my-button
    >
    <div class="header">
      <h2>Добавить организацию</h2>
    </div>
    <organization-form @closeMoreInfo="closeMoreInfo" />
  </div>
  <div v-show="element === 'update'" class="elem">
    <my-button class="closeButton" type="button" @click="closeMoreInfo"
      >x</my-button
    >
    <div class="header">
      <h2>Изменить организацию</h2>
    </div>
    <organization-update-form
      @closeMoreInfo="closeMoreInfo"
      :organizationProp="currentOrganization"
    />
  </div>
</template>

<script>
import OrganizationInfo from "@/components/organization/OrganizationInfo.vue";
import MyButton from "@/components/UI/MyButton.vue";
import OrganizationForm from "@/components/organization/OrganizationForm.vue";
import OrganizationsBlock from "@/components/organization/OrganizationsBlock.vue";
import OrganizationUpdateForm from "@/components/organization/OrganizationUpdateForm.vue";

export default {
  components: {
    OrganizationUpdateForm,
    OrganizationsBlock,
    OrganizationForm,
    MyButton,
    OrganizationInfo,
  },
  data() {
    return {
      element: "table",
      headerOrganization: {
        id: "id",
        name: "name",
        coordinates: "coordinates",
        creationDate: "creationDate",
        type: "type",
        officialAddress: "officialAddress",
        annualTurnover: "annualTurnover",
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
      console.log(this.currentOrganization);
      this.element = "update";
    },
    closeMoreInfo() {
      this.element = "table";
    },
    addOrganization() {
      this.element = "form";
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

.header {
  padding: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.my-button {
  width: 100%;
}
</style>
