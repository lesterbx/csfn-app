<template>
  <page-transparent-header ref="page">
    <ion-page class="ion-page">
      <transparent-header :no-back="true" :no-gradient="true" :title="$t('alerts')"></transparent-header>

      <ion-content ref="alerts-content" :scroll-events="true" class="fullscreen " color="white"
                   @ionScroll="$refs['page'].scrolled($event)">
        <home-header :num="3">
          <div class="h-toolbar-top sm:ios:mb-2"></div>
          <div class="flex flex-col h-full p-4 pt-10 text-left relative">
            <img class="w-56 absolute" src="@/assets/img/empty/alerts.png" style="top: 10px; right: -10px"/>

            <!--
            <div class="rounded-full overflow-hidden shadow ion-activatable relative z-10"
                 style="margin-top: 15%">
                <ion-item>
                    <ion-icon slot="start" color="secondary" name="location-sharp"></ion-icon>
                    <ion-label>{{ address }}</ion-label>
                </ion-item>
                <ion-ripple-effect></ion-ripple-effect>
            </div>
            -->
          </div>
        </home-header>

        <div class="mt-2 mb-2 w-1/3 mx-auto">
          <img src="@/assets/img/icons/wip.svg" style="opacity: 0.15"/>
        </div>
        <span class="font-bold text-xl capitalize opacity-75">{{ $t('coming-soon') }}</span>
        <div class="p-4 opacity-75 text-sm">{{ $t('no-alerts-more') }}</div>
        <div class="pt-20"></div>
      </ion-content>
    </ion-page>
  </page-transparent-header>
</template>
<script lang=ts>
import Vue from 'vue'
import Component from 'vue-class-component'
import Wave from '@/views/components/common/Wave.vue'
import TransparentHeader from '@/views/components/common/TransparentHeader.vue'
import CleanupsList from '@/views/components/home/CleanupsList.vue'
import { locationModule } from '@/store/locationModule'
import { Ref } from 'vue-property-decorator'
import PageTransparentHeader from '@/views/components/common/PageTransparentHeader.vue'
import PlaceholderCard from '@/views/components/home/PlaceholderCard.vue'
import { addressToString } from '@/tools/Utils'
import HomeHeader from '@/views/components/home/HomeHeader.vue'

@Component({
  name: 'alerts-page',
  components: { HomeHeader, PlaceholderCard, PageTransparentHeader, CleanupsList, TransparentHeader, Wave }
})
export default class AlertsPage extends Vue {


  @Ref('alerts-content')
  content: HTMLIonContentElement

  get alerts() {
    return []
    //return cleanupsModule.getAlerts
  }

  get address() {
    return locationModule.getAddress ? addressToString(locationModule.getAddress) : ''
  }

  get coords() {
    return locationModule.getCoords
  }

  init() {
    //cleanupsModule.fetch()
  }

  open(id) {
    this.$router.push('/cleanup/' + id)
  }

  exit() {
    return
  }
}
</script>
<style scoped>

</style>
