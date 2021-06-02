<template>
  <div id="registerWrapper">
    <div id="registerContent">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>用户注册</span>
          <span
            id="checkTips"
            v-text="tips"
            :class="this.state ? this.greenTips : this.redTips"
          ></span>
        </div>
        <div id="registerContentBody">
          <el-input
            id="newusername"
            v-model="newUser.newusername"
            clearable
            @blur="checkUserInform"
          ></el-input>
          <el-input
            id="newpassword"
            v-model="newUser.newpassword"
            show-password
            clearable
          ></el-input>
        </div>
        <div id="registerSubmit">
          <el-button
            id="systemSubmit"
            @click="registerSystem"
            :disabled="!this.state"
            :class="this.state ? this.submit1 : this.submit2"
            >注册</el-button
          >
        </div>
      </el-card>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
const url = "http://localhost:3000";
export default {
  name: "register",
  data() {
    return {
      newUser: {
        newusername: "",
        newpassword: "",
      },
      tips: "",
      redTips: "redTips",
      greenTips: "greenTips",
      state: true,
      submit1: "systemSubmit1",
      submit2: "systemSubmit2",
    };
  },
  methods: {
    checkUserInform() {
      // alert(999)
      Axios.get("/register/check", {
        params: this.newUser,
      }).then((res) => {
        this.tips = res.data.message;
        // alert(res.data.message);
        if (res.data.state == "success") {
          this.state = true;
        } else {
          this.state = false;
        }
      });
    },
    // CORS
    registerSystem() {
      // Axios.post(url + "/register", {
      //   params: this.newUser,
      // }).then(function (resx) {
      //   //请求体 响应体 消息体
      //   console.log(resx);
      // });
      // Axios.get("http://localhost:3000/register", {
      //   params: this.newUser,
      // }).then(function (response) {
      //   alert(response.data);
      // });
      Axios.post(url + "/register", {
        params: this.newUser,
      }).then(function (response) {
        alert(response.data);
      });
    },
  },
};
</script>

<style>
#registerWrapper {
  /* background-color: purple; */
  height: 100%;
}
#registerContent {
  width: 400px;
  margin: 0 auto;
  padding-top: 100px;
}
#systemSubmit {
  display: block;
  margin: 0 auto;
  background-color: #0a9588;
  color: white;
  border-color: #0a9588;
}
.systemSubmit1 {
  display: block;
  margin: 0 auto;
  background-color: #0a9588;
  color: white;
  border-color: #0a9588;
}
.systemSubmit2 {
  display: block;
  margin: 0 auto;
  background-color: #aaa6a6 !important;
  color: white;
  border-color: #aaa6a6 !important;
}
#newpassword {
  margin-top: 5px;
  margin-bottom: 8px;
}
#checkTips {
  /* background-color: blue; */
  margin-left: 45px;
}
.redTips {
  color: red;
}
.greenTips {
  color: green;
}
</style>
