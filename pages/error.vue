<template>
  <div class="app">
    <img src="@/assets/logo.png" alt="" />
    <h2>
      حدث خطأ ما <br />
      سيتم اعادة توجيهك
    </h2>
  </div>
</template>

<style scoped>
.app {
  font-family: ad-rsail;
  width: 100%;
  height: 100vh;
  display: flex;
  text-align: center;
  color: red;
  line-height: 1.4;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
img {
  max-width: 300px;
}
</style>

<script>
export default {
  created() {
    // setTimeout(() => {
    //     window.location.href = "https://alqurain.org"
    // }, 3000);
  },
};
</script>
