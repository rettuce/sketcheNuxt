<template>
  <div class="full">
    <h3 class="txt">
      404 !
    </h3>
  </div>
</template>

<script>
export default {
  layout: "post"
};
</script>

<style lang="css" scoped>
.full {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background-color: red;
}
.txt {
  color: #888888;
  padding: 25px 20px;
  position: relative;
  display: block;
  z-index: 10;
}
</style>
