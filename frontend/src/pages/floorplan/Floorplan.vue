<template>
  <div>
    <svg 
      viewBox="97.416 68 1660 600" 
      xmlns="http://www.w3.org/2000/svg" 
      xmlns:xlink="http://www.w3.org/1999/xlink">
      <base-layer>
        <!-- <control-layer v-if="floorplan.length" :floorplan="floorplan" :entities="entities"/> -->
      </base-layer>
    </svg>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import BaseLayer from "@/pages/floorplan/BaseLayer.vue";
import ControlLayer from "@/pages/floorplan/ControlLayer.vue";
import { Entities } from "@/store/vuex-decorators";

@Component({
  components: {
    BaseLayer,
    ControlLayer
  }
})
export default class Floorplan extends Vue {
  @Entities.State entities;

  created() {
    // this.fetchFloorplan();
  }
}
</script>
