<template>
  <div>
    <b-navbar variant="faded" type="dark">
      <b-navbar-brand tag="h3" class="mb-0">Quiz App</b-navbar-brand>
      <b-navbar-item>Counter : {{ numCorrect }} / {{ numTotal }}</b-navbar-item>
    </b-navbar>
  </div>
</template>

<script>
export default {
  props: ["numCorrect", "numTotal"]
};
</script>

