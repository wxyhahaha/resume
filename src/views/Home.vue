<template>
  <div class="home">
    <Menu />
    <Pdf class="home-pdf" name="name">
      11
    </Pdf>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

import Pdf from '@/components/Pdf.vue';

import Menu from '@/components/Menu.vue';

@Component({
  components: {
    Pdf,
    Menu,
  },
})
export default class Home extends Vue {}
</script>

<style lang="less" scoped>
.home {
  display: flex;
  &-menu {
    width: 20%;
    height: 100%;
  }
  &-pdf {
    width: 80%;
    transform: translateX(20%);
  }
}
</style>
