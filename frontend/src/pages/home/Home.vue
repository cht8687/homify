<template>
  <div class="home-layout">
    <div 
      class="column" 
      v-for="column in 4" 
      :key="column" 
      v-if="columnGroup[column - 1]">
      <el-card 
        class="group-card" 
        :body-style="{ padding: '0' }" 
        v-for="group in columnGroup[column - 1]" 
        :key="group">
        <div slot="header" class="header">
          <span class="card-title">{{ group }}</span>
        </div>
        <div class="device-list" >
          <div 
            class="device-item"
            v-for="entity in grouped[group]"
            :key="entity.entityId">
            <device-switch 
              v-if="entity" 
              :entity="entity" 
              :state-info="statePool[entity.entityId]"
              :online="onlinePool[entity.entityId]"
              @show-info="openInfoModal(entity)"/>
          </div>
        </div>
      </el-card>
    </div>
    <info-modal 
      ref="infomodal" 
      :state-pool="statePool" 
      :online-pool="onlinePool"/>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import { Entities } from "@/store/vuex-decorators";
import DeviceSwitch from "@/components/DeviceSwitch/DeviceSwitch.vue";
import InfoModal from "@/components/Modal/InfoModal.vue";

@Component({
  components: {
    DeviceSwitch,
    InfoModal
  }
})
export default class Home extends Vue {
  @Entities.State grouped;

  @Entities.State columnGroup;

  @Entities.State statePool;

  @Entities.State onlinePool;

  openInfoModal(entity) {
    (this.$refs.infomodal as any).open(entity);
  }
}
</script>

<style lang="scss">
.home-layout {
  display: flex;
  flex-wrap: wrap;
  .column {
    flex: 25%;
    padding: 0 4px;
    max-width: 500px;
  }
  .group-card {
    flex: 1;
    margin-bottom: 1rem;
    .el-card__header {
      border-bottom: none;
    }
    .card-title {
      text-transform: capitalize;
    }
  }
  .device-list {
    width: 100%;
    .device-item {
      padding: 0 10px;
    }
  }
  .popup-body {
    position: relative;
    box-sizing: border-box;
    text-align: center;
    background-color: white;
  }
}
@media only screen and (min-width: 450px) {
  .group-card {
    min-width: 400px;
  }
}

@media only screen and (max-width: 768px) {
  .home-layout {
    justify-content: center;
  }
}
</style>


