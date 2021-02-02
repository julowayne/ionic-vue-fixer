<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title class="ion-text-center">Money converter</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="container">
        <Search @amountAsked="getAmount"></Search>
        <results v-if="moneyAsked" :moneyAsked="moneyAsked"></results>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import Results from '@/components/Results.vue';
import Search from '@/components/Search.vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Results,
    Search
  },
  data(){
    return {
      moneyAsked: null,
    }
  },
  methods: {
    getAmount(data){
     this.moneyAsked = data
    }
  }
});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

</style>