<template>
  <p class="copyright">This game owned by MucMuc Team in Vue 3 course for begginers - <a href="#">view here</a> </p>
</template>

<script>
export default {
  name: 'CoppyrightScreen',
}
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: #212121;
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}
</style>