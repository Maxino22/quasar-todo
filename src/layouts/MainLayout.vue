<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todaysDate }}</div>
      </div>
      <q-img src="../statics/mountains.jpg" class="header-image absolute-top" />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="600"
    >
      <q-scroll-area
        style="
          height: calc(100% - 192px);
          margin-top: 192px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Todo </q-item-section>
          </q-item>
          <q-item to="/help" clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="../statics/mountains.jpg"
        style="height: 192px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://www.maxino.xyz/assets/max.f9b8fe05.png" />
          </q-avatar>
          <div class="text-weight-bold">Maxwell Muhanda</div>
          <div>@Maxino22</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script lang="ts" setup>
import { date } from 'quasar';
import { computed, ref } from 'vue';

const todaysDate = computed(() => {
  let timestamp = Date.now();
  return date.formatDate(timestamp, 'dddd D MMMM');
});
const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%);
}
</style>
