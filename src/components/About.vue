<template>
  <div class="about">
    <h1>Hello {{ their_name }}, this is about page</h1>
    <p>Some about info</p>
  </div>
</template>

<script>
export default {
  name: "About",
  props: {},
  data() {
    return {
      their_name: this.$route.params.name,
    };
  },
};
</script>