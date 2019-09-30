<template>
    <div id="login-background">
        <div id="login-box">
            <h2 id="title">VR 대여 프로그램</h2>
            <div id="login-form">
                <div class="input-group input-margin">
                    <input type="text"
                           class="form-control"
                           placeholder="ID"
                           v-model="id"
                           @focusout="validationId()">
                </div>
                <p class="validation-message">
                    {{idValidationMessage}}
                </p>


                <div class="input-group input-margin">
                    <input type="password"
                           class="form-control"
                           placeholder="Password"
                           v-model="password"
                           @focusout="validationPassword()">
                </div>
                <p class="validation-message">
                    {{passwordValidationMessage}}
                </p>
            </div>

            <button type="button"
                    id="button"
                    class="btn btn-primary btn-lg btn-block">로그인
            </button>

            <router-link id="join"
                         to="/join">회원가입
            </router-link>
        </div>
    </div>
</template>

<script lang="ts">
  import {Component, Vue} from "vue-property-decorator";

  @Component({
    components: {}
  })
  export default class Home extends Vue {
    public id: string = "";
    public idValidationMessage: string = "";

    public password: string = "";
    public passwordValidationMessage: string = "";

    public validationId(): void {
      if (this.id.length < 4 || this.id.length >= 20) {
        this.idValidationMessage = "아이디의 길이는 4 ~ 20 입니다.";
        return;
      }

      const regExp = /^[a-zA-Z0-9]+$/;
      const result: boolean = regExp.test(this.id);
      this.idValidationMessage = result ? "" : "아이디는 영문자 또는 숫자만 가능합니다.";
    }

    public validationPassword(): void {
      if (this.password.length < 8 || this.password.length >= 20) {
        this.passwordValidationMessage = "비밀번호의 길이는 8 ~ 20 입니다.";
        return;
      }

      const checkNumber: number = this.password.search(/[0-9]/g);
      const checkEnglish: number = this.password.search(/[a-zA-Z]/g);
      const checkSymbol: number = this.password.search(/[!@#$%^&*()]/g);
      if (checkNumber < 0 || checkEnglish < 0 || checkSymbol < 0) {
        this.passwordValidationMessage = "비밀번호는 영문자, 숫자, 특수기호(-_=+ 제외)가 혼용되어야 합니다.";
        return;
      }

      const regExp = /^[a-zA-Z0-9!@#$%^&*()]+$/;
      const result: boolean = regExp.test(this.password);
      this.passwordValidationMessage = result ? "" : "비밀번호는 영문자 또는 특수기호(-_=+ 제외)만 가능합니다.";
    }
  }
</script>

<style>
    #login-background {
        height: 100vh;
        background-color: #f2f2f2;
    }

    #login-box {
        width: 400px;
        text-align: center !important;
        margin: auto;
        position: relative;
        top: 100px;
    }

    #login-form {
        position: relative;
        top: 20px;
    }

    #button {
        position: relative;
        top: 40px;
    }

    #join {
        position: relative;
        top: 60px;
    }

    .input-margin {
        margin: 5px 0;
    }

    .validation-message {
        color: maroon;
        margin: 0 10px;
        text-align: left !important;
        font-size: 14px;
    }
</style>
