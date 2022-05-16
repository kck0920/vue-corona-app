<template>
  <h2 class="content-title">{{ content.label }}</h2>
  <component :is="targetComponent"></component>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { defineAsyncComponent } from 'vue';
export default {
  name: 'mainContent',
  props: {
    content: {
      type: Object,
      default() {
        return {
          label: 'Test Menu',
          path: 'Test',
          index: 'TestMenu',
        };
      },
    },
  },
  data() {
    return {
      targetComponent: null,
    };
  },
  watch: {
    content: {
      deep: true,
      handler: function (newValue) {
        this.targetComponent = defineAsyncComponent(() => 
          import(`@/components/${newValue.path}/${newValue.index}`)
        );
      },
    },
  },
};
</script>

<style></style>
