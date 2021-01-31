<template>
  <div>
    <ion-searchbar placeholder="Enter your amount in EU" v-model="amountAndDevise.query"></ion-searchbar>
    <ion-list>
        <ion-item>
          <ion-label>Convert in</ion-label>
          <ion-select v-model="amountAndDevise.name" :placeholder="symbols.AED">
            <ion-select-option v-for="(symbol, name) in symbols" :value="name" :key="symbol"> {{ symbol }}</ion-select-option>
          </ion-select>
        </ion-item>
    </ion-list>
    <section>
      <ion-button :disabled="!amountAndDevise.query || !amountAndDevise.name" @click="getAmount">Convert</ion-button>
    </section>
  </div>
</template>

<script>
import { IonList, IonSearchbar, IonItem, IonLabel, IonSelect, IonSelectOption, IonButton } from '@ionic/vue';
import axios from 'axios';
  export default {
    components: {
      IonList,
      IonSearchbar,
      IonItem,
      IonLabel,
      IonSelect,
      IonSelectOption,
      IonButton
    },
    data() {
      return {
        symbols: [],
        amountAndDevise: {
          query: "",
          name: ""
        }
      }
    },
    methods: {
      getFixerList(){
      axios.get(`http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_FIXER_API_KEY}`)
        .then((response)=> {
          this.symbols = response.data.symbols
        })
        .catch(function (error) {
          console.log(error);
        });
      },
      getAmount(){
        this.$emit('amountAsked', this.amountAndDevise)
      }
    },
    mounted(){
      this.getFixerList();
    }
  }
</script>

<style scoped>
  ion-button {
    --box-shadow: 0 .125rem .25rem rgba(0,0,0,.075)!important;
    --color: white;
    --background: #20c997;
    --background-activated: #20c997;
    width: 75%;
  }
  section {
    margin-top: 1em;
    margin-bottom: 2.5em;
  }

</style>