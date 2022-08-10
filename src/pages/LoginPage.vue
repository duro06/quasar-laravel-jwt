<template>
  <q-page class="flex flex-center">
    <div class="left-section">
      <div class="warna-text"><h3>Apotek</h3></div>
      <div>
        <p>Tempat yang tepat untuk membeli obat</p>
        <p>Tidak menjual jamu, karena bukan depot jamu</p>
      </div>
    </div>
    <div class="right-section">
      <q-card class="my-card">
        <q-card-section>
          <q-input
            filled
            outlined
            dense
            v-model="mail"
            placeholder="e-mail"
            type="email"
            bottom-slots
            :error="errorCheck"
            @update:model-value="mailUpdate"
          >
            <template v-slot:error> incorrect mail format </template>
          </q-input>
          <q-input
            filled
            outlined
            dense
            v-model="password"
            placeholder="password"
            :type="isPwd ? 'password' : 'text'"
          >
            <template v-slot:append>
              <div style="font-size: 0.8em">
                <q-icon
                  :name="isPwd ? 'visibility_off' : 'visibility'"
                  class="cursor-pointer"
                  @click="passwordVisible"
                />
              </div>
            </template>
          </q-input>
          <!-- <q-input v-model="password" filled type="password" hint="Password" /> -->
        </q-card-section>
        <q-card-actions class="center" vertical>
          <q-btn color="primary" glossy no-caps @click="masuk">Masuk</q-btn>
          <q-btn
            text-color="red"
            icon="fa-brands fa-google"
            label="Masuk dengan Google"
            no-caps
          />
        </q-card-actions>
      </q-card>
    </div>
  </q-page>
</template>
<script setup>
import { ref } from "vue";
//----------undef--------//
let reg =
  '/^(([^<>()[]\\.,;:s@"]+(.[^<>()[]\\.,;:s@"]+)*)|(".+"))@(([[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}])|(([a-zA-Z-0-9]+.)+[a-zA-Z]{2,24}))$/';
//----------------Mail--------//
const mail = ref("wawan@gmail.com");
const errorCheck = ref(false);
//--validasi email agar formatnya benar--//
function mailUpdate() {
  const toTest = mail.value;
  if (toTest != "") {
    // nyoba pake reg.test() ga bisa, bisanya dilangsung seperti dibawah ini. kalo pake reg.test() error, bukan fungsi katanya. ga ada this nya sih
    if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(toTest)) {
      errorCheck.value = false;
      console.log(true);
    } else {
      errorCheck.value = true;
      console.log(false);
      // console.log(reg);
    }
  }
}
//-------Mail End-----------------//
//--------------Password------//
const password = ref("123456789");
const isPwd = ref(true);
let passwordVisible = () => {
  isPwd.value = !isPwd.value;
};
//-----------Password End-------//
//-------- take data and submit to back end--//
const masuk = () => {
  console.log(mail.value);
  console.log(password.value);
};
//-------- end of take data and submit to back end--//
</script>
<style scoped>
.left-section {
  margin: 10px;
  text-align: left;
}
.right-section {
  margin: 10px;
}
</style>
