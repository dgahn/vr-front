<template>
    <div id="join-background">
        <div id="join-box">
            <h2 id="title">VR 대여 프로그램</h2>
            <div id="join-form">
                <div class="input-group input-margin">
                    <input type="text"
                           class="form-control"
                           placeholder="Name"
                           v-model="name"
                           @focusout="validationName()">
                </div>
                <p class="validation-message">
                    {{nameValidationMessage}}
                </p>

                <div class="input-group input-margin">
                    <input type="text"
                           class="form-control"
                           placeholder="Email"
                           v-model="email"
                           @focusout="validationEmail()">
                </div>
                <p class="validation-message">
                    {{emailValidationMessage}}
                </p>

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

            <div id="btn-box"
                 class="row">
                <div class="col">
                    <router-link class="router-link"
                                 to="/">
                        <button type="button"
                                class="btn btn-primary btn-lg btn-block">
                            join
                        </button>
                    </router-link>
                </div>
                <div class="col">
                    <router-link class="router-link"
                                 to="/">
                        <button type="button"
                                class="btn btn-secondary btn-lg btn-block">
                            cancel
                        </button>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
  import {Vue, Component} from "vue-property-decorator";

  @Component
  export default class Joint extends Vue {
    public name: string = "";
    public nameValidationMessage: string = "";

    public email: string = "";
    public emailValidationMessage: string = "";

    public id: string = "";
    public idValidationMessage: string = "";

    public password: string = "";
    public passwordValidationMessage: string = "";

    public validationName(): void {
      if (this.name.length < 2 || this.name.length >= 20) {
        this.nameValidationMessage = "이름의 길이는 2 ~ 20 입니다.";
        return;
      }

      const regExp = /^[가-힣a-zA-Z]+$/;
      const result: boolean = regExp.test(this.name);
      this.nameValidationMessage = result ? "" : "이름은 한글 또는 영문자만 가능합니다.";
    }

    public validationEmail(): void {
      const regExp = /^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/;
      const result: boolean = regExp.test(this.email);
      this.emailValidationMessage = result ? "" : "이메일 형식에 맞지 않습니다.";
    }

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

<style scoped>
    #title {
        margin-bottom: 20px;
    }

    #join-background {
        height: 100vh;
        background-color: #f2f2f2;
    }

    #join-box {
        width: 400px;
        text-align: center !important;
        margin: auto;
        position: relative;
        top: 100px;
    }

    #btn-box {
        position: relative;
        top: 19px;
    }

    .validation-message {
        color: maroon;
        margin: 0 10px;
        text-align: left !important;
        font-size: 14px;
    }

    .input-margin {
        margin: 5px 0;
    }

    .router-link {
        color: white;
    }
</style>
