<template>
  <el-container class="main">
    <el-header><BasicHeader /></el-header>
    <el-container>
      <el-aside :width="menuWidth"
        ><SideMenu
          :isCollapse="isCollapse"
          @menuSelect="
            (item) => {
              $emit('menuSelect', item);
            }
          "
      /></el-aside>
      <el-main><slot></slot></el-main>
    </el-container>
  </el-container>
</template>

<script>
import BasicHeader from './BasicHeader';
import SideMenu from './SideMenu';
// eslint-disable-next-line no-unused-vars
import useBreakpoint from '@/composable/useBreakpoint';
import { computed } from 'vue';
export default {
  name: 'basicLayout',
  components: {
    BasicHeader,
    SideMenu,
  },
  setup() {
    // eslint-disable-next-line no-unused-vars
    const { type } = useBreakpoint();
    const isCollapse = computed(() => type.value === 'sm');
    // eslint-disable-next-line no-unused-vars
    const menuWidth = computed(() => (isCollapse.value ? '65px' : '200px'));
    return {
      isCollapse,
      menuWidth,
    };
  },
};
</script>

<style>
.el-header {
  background: #409eff;
  color: #fff;
  display: flex;
  align-items: center;
}

.main {
  height: 100%;
}
</style>
