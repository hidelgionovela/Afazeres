
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

        <q-toolbar-title>
           <div class="q-px-lg q-pt-xl q-mb-md" >
            <div class = "text-h3">Afazeres </div>
            <div class = "text-subtitle"> Segunda-Feira 20 de Junho </div>
            
          </div>
          <q-img  src="../assets/afazer.jpeg"
          class="header-image absolute-top" />
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
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
        <q-item-label
          header
        >
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
<q-scroll-area style="height: calc(100% - 192px); margin-top: 152px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Afazeres
              </q-item-section>
            </q-item>

    
            <q-item clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Ajuda
              </q-item-section>
            </q-item>

            
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/afazer.jpeg" style="height: 195px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../assets/hidell.jpg">
            </q-avatar>
            <div class="text-weight-bold">Hidelgio Novela</div>
            <div>@hidelgio_novela</div>
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
import { computed, defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import{date} from 'quasar'

const linksList = [];

// import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style lang="scss">
.header-image{
  height: 100%;
  z-index: -1;
  opacity: 0.4;
  filter: grayscale(100%);
}

</style>