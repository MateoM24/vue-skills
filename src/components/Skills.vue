<template>
  <div class="hello">
    <div class="holder">
      <validation-observer ref="observer" @submit.prevent="addSkill()">
        <form @submit.prevent="addSkill">
          <validation-provider v-slot="{ errors }" rules="min:3">
            <input
              type="text"
              placeholder="Enter skill you have"
              v-model="skill"
              name="skill"
            />
            <transition
              mode="out-in"
              enter-active-class="animate__animated animate__flipInX"
              leave-active-class="animate__animated animate__flipOutX"
            >
              <div class="alert" v-if="errors[0]">
                {{ errors[0] }}
              </div>
            </transition>
          </validation-provider>
        </form>
      </validation-observer>

      <ul>
        <transition-group
          name="list"
          enter-active-class="animate__animated animate__bounceInUp"
          leave-active-class="animate__animated animate__bounceOutDown"
        >
          <li v-for="(data, index) in skills" :key="index">
            {{ data.skill }}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>
      <p>This are the skills that you possess</p>
    </div>
  </div>
</template>

<script>
import { ValidationProvider, extend, ValidationObserver } from "vee-validate";

extend("min", {
  validate(value, args) {
    if (value.length >= args.length) {
      return true;
    }
    return "The {_field_} should be at leat 3 letters long";
  },
  computesRequired: true,
  params: ["length"],
});

export default {
  name: "Skills",
  components: {
    ValidationProvider,
    ValidationObserver,
  },
  props: {},
  data() {
    return {
      skills: [{ skill: "Vue.js" }, { skill: "FrontEnd developer" }],
      skill: "",
    };
  },
  methods: {
    async addSkill() {
      const isValid = await this.$refs.observer.validate();
      if (!isValid) {
        return;
      }
      this.skills.push({ skill: this.skill });
      this.skill = "";
    },
    remove(index) {
      this.skills.splice(index, 1);
    },
  },
};
</script>
  
<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
  background: #fff;
}
ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}
ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3ebe33f5;
  margin-bottom: 2px;
  color: #3e5252;
}
p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}
.container {
  box-shadow: 0px 0px 40px lightgray;
}
input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}
.alert {
  height: 1em;
  margin: 0;
  padding: 0.4em;
}
i {
  float: right;
  cursor: pointer;
}
</style>
