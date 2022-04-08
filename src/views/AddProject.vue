<template>
  <div class="logo-area">
    <img src="../assets/logo2.png" />
    <div>
      <router-link :to="{ name: 'Home' }" class="back-button"
        >Return to List Page</router-link
      >
    </div>
  </div>
  <form @submit.prevent="handleSubmit" class="addProject">
    <div>
      <label :class="{ invalid: userNameSurnameValidity === 'invalid' }"
        >Name Surname</label
      >
      <input
        :class="{ invalidinput: userNameSurnameValidity === 'invalid' }"
        type="text"
        v-model.trim="namesurname"
        @blur="validateNameSurname(namesurname)"
        placeholder="Enter name and surname"
      />
      <div v-if="userNameSurnameValidity === 'invalid'" class="error">
        Please enter a valid name!
      </div>
    </div>
    <div>
      <label :class="{ invalid: userCountryValidity === 'invalid' }"
        >Country</label
      >
      <input
        :class="{ invalidinput: userCountryValidity === 'invalid' }"
        type="text"
        v-model.trim="country"
        @blur="validateCountry(country)"
        placeholder="Enter a country"
      />
      <div v-if="userCountryValidity === 'invalid'" class="error">
        Please enter a valid country!
      </div>
    </div>
    <div>
      <label :class="{ invalid: userCityValidity === 'invalid' }">City</label>
      <input
        :class="{ invalidinput: userCityValidity === 'invalid' }"
        type="text"
        v-model.trim="city"
        @blur="validateCity(city)"
        placeholder="Enter a city"
      />
      <div v-if="userCityValidity === 'invalid'" class="error">
        Please enter a valid city!
      </div>
    </div>
    <div>
      <label :class="{ invalid: userEmailValidity === 'invalid' }">Email</label>
      <input
        :class="{ invalidinput: userEmailValidity === 'invalid' }"
        type="email"
        v-model="email"
        @blur="validateEmail(email)"
        placeholder="Enter a e-mail(abc@xyz.com)"
      />
      <div v-if="userEmailValidity === 'invalid'" class="error">
        Please enter a valid email!
      </div>
    </div>
    <div>
      <button
        :class="{
          disabledbutton:
            userNameSurnameValidity === 'invalid' ||
            userCityValidity === 'invalid' ||
            userCountryValidity === 'invalid' ||
            userEmailValidity === 'invalid',
        }"
      >
        Add
      </button>
    </div>
  </form>
  <div class="errorshere" v-if="errors.length">
    <div>
      <div>
        <span>Error while adding link element</span>
        <ul>
          <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
        </ul>
      </div>
      <div class="error-name">Errors</div>
      <img @click="cancelError" src="../assets/delete.svg" />
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  data() {
    return {
      namesurname: "",
      country: "",
      city: "",
      email: "",
      date: "",
      errors: [],
      userNameSurnameValidity: "pending",
      userCountryValidity: "pending",
      userCityValidity: "pending",
      userEmailValidity: "pending",
    };
  },
  methods: {
    handleSubmit() {
      let projecthere = {
        namesurname: this.namesurname,
        Email: this.email,
        Date: new Date().toLocaleDateString(),
        Country: this.country,
        City: this.city,
        id: uuidv4(),
      };
            this.errors = [];
      if (!this.validateNameSurname(this.namesurname)) {
        this.errors.push(
          "Name Surname should be (only letters, min 4 – max 60 character)"
        );
      }
      if (!this.validateCountry(this.country)) {
        this.errors.push(
          "Country should be (only letters, min 2 – max 40 character)"
        );
      }
      if (!this.validateCity(this.city)) {
        this.errors.push(
          "City should be (only letters, min 2 – max 40 character)"
        );
      }
      if (!this.validateEmail(this.email)) {
        this.errors.push("Email should be validation.");
      } else {
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(projecthere),
      })
        .then(() => {
          if (!this.errors.length) {
            this.$router.push("/");
            return true;
          }
        })
        .catch((err) => {
          console.log(err);
        })
      }
    },
    validateNameSurname(namesurname) {
      var valid = /^[a-z A-ZiİçÇşŞğĞÜüÖö]{4,60}$/;
      if (!valid.test(namesurname)) {
        this.userNameSurnameValidity = "invalid";
      } else {
        this.userNameSurnameValidity = "valid";
      }
      return valid.test(namesurname);
    },

    validateCountry(country) {
      var valid = /^[a-zA-ZiİçÇşŞğĞÜüÖö]{2,40}$/;
      if (!valid.test(country)) {
        this.userCountryValidity = "invalid";
      } else {
        this.userCountryValidity = "valid";
      }
      return valid.test(country);
    },
    validateCity(city) {
      var valid = /^[a-zA-ZiİçÇşŞğĞÜüÖö]{2,40}$/;
      if (!valid.test(city)) {
        this.userCityValidity = "invalid";
      } else {
        this.userCityValidity = "valid";
      }
      return valid.test(city);
    },
    validateEmail(email) {
      var valid =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if (!valid.test(email)) {
        this.userEmailValidity = "invalid";
      } else {
        this.userEmailValidity = "valid";
      }
      return valid.test(email);
    },
    cancelError() {
      this.errors = [];
    },
  },
};
</script>

<style lang="scss" scoped>
.logo-area {
  margin: 27px 0px 0px 37px;
  display: flex;
  justify-content: flex-start;
  align-items: center;

  div {
    margin-left: 45px;
  }
}
.back-button {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 28px;
  color: #484848;
  text-decoration: none;

  &:hover {
    text-decoration: underline;
  }
}
.addProject {
  padding: 20px;
  border-radius: 10px;
  max-width: 1200px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .invalid {
    color: #ff0000;
  }
  label {
    display: block;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 21px;
    color: #686868;
    margin: 10px 0px 10px 7px;
  }
  .invalidinput {
    border: 1.5px solid #ff0000;

    &::placeholder {
      color: #ff0000;
    }
  }
  input {
    width: 82vw;
    height: 46px;
    max-width: 590px;
    box-sizing: border-box;
    background: #ffffff;
    border: 1.5px solid #484848;
    border-radius: 12px;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    text-indent: 17px;
    line-height: 21px;

    &::placeholder {
      color: rgba(100, 100, 100, 0.5);
    }
    &:hover {
      background: rgba(100, 100, 100, 0.08);
      border: 2px solid rgba(72, 72, 72, 0.6);
    }
  }
  .error {
    color: red;
    margin-top: 10px;
  }
  .disabledbutton {
    pointer-events: none;
    opacity: 0.5;
  }
  button {
    width: 138px;
    height: 46px;
    background: #204080;
    border: none;
    border-radius: 12px;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 21px;
    margin-top: 30px;
    text-align: center;
    color: #ffffff;

    &:hover {
      background: #4f75c2;
    }
  }
  & > div:last-child {
    display: flex;
    justify-content: flex-end;
    width: 82vw;
    max-width: 590px;
  }
}
.errorshere {
  width: 375px;
  min-height: 123px;
  background: #c4c4c4;
  border-radius: 8px;
  margin-left: auto;
  position: fixed;
  bottom: 10px;
  right: 10px;

  & > div:first-child {
    padding: 5px 25px;
    display: flex;
    min-height: inherit;
    justify-content: space-between;
    align-items: center;
    position: relative;
  }

  span {
    font-family: "Inter";
    font-style: normal;
    font-weight: 700;
    font-size: 14px;
    line-height: 36px;
    color: #090a0a;
  }

  li {
    font-family: "Inter";
    font-style: normal;
    font-weight: 400;
    font-size: 13px;
    line-height: 24px;
    color: #090a0a;
  }
  .error-name {
    width: 70px;
    height: 32px;
    background: #ff4e78;
    border-radius: 48px;
    color: #fff;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  img {
    position: absolute;
    right: 10px;
    top: 10px;
  }
}
</style>
