<template>
  <v-container>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row>
        <!--  -->
        <v-col cols="6">
          <v-text-field
            v-model="name"
            :counter="30"
            :rules="nameRules"
            label="ชื่อ"
            required
          ></v-text-field
        ></v-col>
        <!-- นามสกุล -->
        <v-col cols="6">
          <v-text-field
            v-model="lastname"
            :counter="30"
            :rules="lastnameRules"
            label="นานสกุล"
            required
          ></v-text-field
        ></v-col>
      </v-row>
      <v-checkbox
        v-model="checkbox"
        :rules="checkboxRules"
        label="ยอมรับเงื่อนไข"
        required
      ></v-checkbox>
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        สมัครสมาชิก
      </v-btn>
      <v-btn color="error" class="mr-4" @click="reset">
        เคลียร์
      </v-btn>
      <v-row>
        <v-col cols="12">
          <!-- ตารางแสดงข้อมูล -->
          <v-card>
            <v-card-title>
              ข้อมูลลูกค้า
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-data-table
              :headers="headers"
              :items="desserts"
              :search="search"
            ></v-data-table>
          </v-card>
        </v-col>
      </v-row>
      <!-- <v-btn
      color="warning"
      @click="resetValidation"
    >
      เคลียร์การตรวจสอบ
    </v-btn> -->
    </v-form>
  </v-container>
</template>
<script>
import axios from 'axios';
export default {
  data: () => ({
    valid: false,
    name: "",
    nameRules: [
      v => !!v || "กรุณากรอกชื่อ",
      v => (v && v.length <= 30) || "ชื่อต้องมีขนาดไม่เกิน 30 ตัวอักษร"
    ],
    lastname: "",
    lastnameRules: [
      v => !!v || "กรุณากรอกนามสกุล",
      v => (v && v.length <= 30) || "นามสกุลต้องมีขนาดไม่เกิน 30 ตัวอักษร"
    ],
    checkboxRules: [v => !!v || "คุณต้องกรอกยอมรับเงื่อนนไขก่อนสมัครสมาชิก"],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    sex: ["ชาย", "หญิง"],
    checkbox: false,
    a_number: "",
    a_group: "",
    a_road: "",
    a_lane: "",
    a_subdis: "",
    a_dis: "",
    a_province: "",
    addressRules: [
      v => !!v || "กรุณากรอกข้อมูล",
      v => (v && v.length <= 20) || "ต้องมีความยังไม่เกิน 20 ตัวอักษร"
    ],
    search: "",
    headers: [ {
        text: "ชื่อ - นามสกุล",
        value: "fullname"},
      { text: "เบอณ์โทรศัทพ์", value: "tel" },
      { text: "อีเมล", value: "email" },
      { text: "เพศ", value: "sex" },
      { text: "ที่อยู่", value: "address" }
    ],
    desserts: []
  }),
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        //   console.log(this.name);
        //   console.log(this.lastname);
        //   console.log(this.email);
        //   console.log(this.tel);
        //   console.log(this.select);
        //   console.log(this.a_number);
        //   console.log(this.a_group);
        //   console.log(this.a_lane);
        //   console.log(this.a_road);
        //   console.log(this.a_subdis);
        //   console.log(this.a_dis);
        //   console.log(this.a_province);
      // // axios.get('http://localhost:3000/api/students/show').then((res)=>{
      //   console.log(res)
      // });

      axios.post('http://localhost:3000/api/customers/',{
            "c_name": this.name,
            "c_lastname": this.lastname,
      }).then((res)=>{
        console.log(res)
      });


        this.desserts.push({
            fullname:`${this.name}${this.lastname}`,
            });
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>
<style></style>