<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
           @click="toggleLeftDrawer "
          icon="menu"
          aria-label="Menu"
        />

        <q-toolbar-title>
          <div style="line-height: 5rem" class="q-px-lg q-pt-xl q-mb-md">
            <div class="text-h4">Tarefas</div>
            <div class="text-subtitle">{{ todaysDate }}</div>
          </div>
          <q-img
            src="../assets/afazer.jpeg"
            class="header-image absolute-top"
          />
        </q-toolbar-title>
        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      :width="250"
      :breakpoint="600"
    >
      <q-list>
        <q-item-label header> Essential Links </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>

      <!-- inicio area lateral do menu -->
      <q-scroll-area
        style="
          height: calc(90% - 300px);
          margin-top: 130px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item to="/" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Tarefas </q-item-section>
          </q-item>

          <q-item to="/help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Ajuda </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
      <!-- fim area lateral do menu -->

      <q-img
        class="absolute-top"
        src="../assets/afazer.jpeg"
        style="height: 184px"
      >
        <div class="absolute-bottom text-primary" style="top: 0px">
          <q-avatar size="59px" class="q-mb-sm">
            <img src="../assets/hidel1.jpg" />
          </q-avatar>
          <div class="text-weight-bold">Hidélgio Novela</div>
          <div>@hidell_9la</div>
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

<script>
import { computed, defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";
import { date } from "quasar";

const linksList = [];

// import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  computed: {
    todaysDate() {
      let timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd DD of MMMM YYYY");
    },
  },
});
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.6;
  filter: grayscale(100%);
}
</style>
