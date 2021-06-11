<template>
  <div class="hello">
    <div class="holder">
      <ul>
        <li v-for="(data, index) in skills" :key="index">{{ data.skill }}.</li>
      </ul>
      <p>This are the skills that you possess</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  props: {},
  data() {
    return {
      skills: [{ skill: "Vue.js" }, { skill: "FrontEnd developer" }],
      showAlert: true,
      alertObject: {
        alert: true,
      },
    };
  },
};
</script>

<style scoped>
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
</style>
