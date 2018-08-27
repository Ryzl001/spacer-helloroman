<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />

  </div>
</template>

<script>
import Claim from '@/components/Claim';  // alias który od razu wskazuje na rootowy folder src
import SearchInput from '@/components/SearchInput';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
  }
}
</script>
<style lang="scss" scoped>
//Fonts
// @import url('https://fonts.googleapis.com/css?family=Montserrat');

  .wrapper {
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-image: url('../assets/heroimage.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0%;
  }
</style>
