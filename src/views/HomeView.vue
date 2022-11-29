<script lang="ts" setup>
import { reactive, ref } from "vue";

/**
 * set up data
 */
const data = reactive({
  id: "",
  password: "",
  companyId: "",
  selectCompanies: []
});
const saveSetting = reactive({
  id: false,
  option: false
});
const authForm = ref(null);

const rules = {
  idRules: [
    (v: string) => !!v || "아이디는 필 수 입력입니다",
    (v: string) => (v && v.length <= 10) || "10를 초과해서 입력할 수 없습니다."
  ],
  passwordRules: [
    (v: string) => !!v || "비밀번호는 필수 입력입니다",
    (v: string) => (v && v.length <= 10) || "10자리를 초과해서 입력할 수 없습니다"
  ],
  companyRules: [
    (v: string) => !!v || "회사선택은 필수 입니다."
  ]
};


/**
 * @description
 * 서버로 부터 선택한 자음을 바탕으로 회사 목록을 가져옵니다.
 */
async function requestCompanyListsByConsonant(consonant: string) {

  return;
}

async function handleClickLogin() {

}

function validate() {
}
</script>

<template>
  <v-form ref="authForm">
    <v-card class="auth-card pa-3">
      <v-card-title>
        <v-icon class="mr-2 light-navy-blue">mdi-send</v-icon>
        <span class="light-navy-blue fw-semi-bold">XID 메세징 서비스</span>
      </v-card-title>
      <v-card-text>
        <!--   radio buttons -->
        <radio-button-group @change:item="requestCompanyListsByConsonant"></radio-button-group>
      </v-card-text>
      <v-card-text>
        <v-select
          density="compact"
          variant="underlined"
          v-model="data.companyId"
          :items="data.selectCompanies"
          :rules="rules.companyRules"
          item-text="companyName"
          item-value="companyId"
        ></v-select>
        <v-text-field density="compact" variant="underlined" label="ID" v-model="data.id" :rules="rules.idRules"
                      required></v-text-field>
        <v-text-field density="compact" variant="underlined" color="primary" label="PW" type="password" :rules="rules.passwordRules"
                      v-model="data.password"
                      required></v-text-field>
      </v-card-text>
      <v-card-text class="d-flex">
        <v-checkbox v-model="saveSetting.option" density="compact" hide-details label="설정저장"></v-checkbox>
        <v-checkbox v-model="saveSetting.id" density="compact" hide-details label="아이디저장"></v-checkbox>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn class="light-navy-button" variant="outlined"  @click="handleClickLogin">로그인</v-btn>
      </v-card-actions>
    </v-card>
  </v-form>
</template>

<style scoped lang="scss">
.auth-card {
  border-radius: 41px 0 0 41px !important;
}
</style>
