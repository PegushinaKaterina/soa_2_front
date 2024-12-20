<template>
  <div class="app">
    <div class="header">
      <h2>Организации</h2>
    </div>
    <div class="main">
      <organization-page class="appElement" />
    </div>
  </div>
</template>

<script>
import OrganizationPage from "@/components/organization/OrganizationPage.vue";

export default {
  components: {
    OrganizationPage,
  },
  name: "App",
};
</script>

<style scoped>
*:global(*) {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 7px;
  background-color: #d7d4c9;
  font-family: "Courier New";
  font-weight: bolder;
  color: black;
}

.app {
  height: 700px;
  --text-size: 12px;
  --text-size-header: 30px;
  --padding-size: 10px;
  --button-size: 110px;
  --element-form-text-size: 12px;
  width: 100%;
  padding: var(--padding-size);
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}

.main {
  height: 100%;
  font-size: var(--text-size);
  display: flex;
  justify-content: center;
  flex-direction: row;
}

.appElement {
  height: 100%;
  display: flex;
  flex-direction: column;
  width: 70%;
}

.header {
  width: 100%;
  height: 20%;
  text-align: center;
  font-size: var(--text-size-header);
  margin-bottom: 10px;
}
</style>
