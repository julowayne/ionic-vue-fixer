<template>
  <div>
    <ion-card>
      <ion-col>
      <ion-card-content>
          <div>
            The converted amount is : {{ convertedAmount }} {{ moneyAsked.name}}
          </div> 
      </ion-card-content>
      </ion-col>
    </ion-card>
  </div>
</template>

<script>
import { IonCard, IonCol, IonCardContent} from '@ionic/vue';

import axios from 'axios';
  export default {
  components: {
    IonCard,
    IonCol,
    IonCardContent
  },
  props: {
    moneyAsked: Object
  },
  data(){ 
    return {
      convertedAmount: 0,
      rate: 0
    }
  },
  methods: {
    getFixerConversion(){
      axios.get(`http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_FIXER_API_KEY}&symbols=${this.moneyAsked.name}`)
        .then((response)=> {
          this.rate = response.data.rates[this.moneyAsked.name]
          this.convertedAmount =  Math.round((this.rate * this.moneyAsked.query) * 100) / 100
        })
        .catch(function (error) {
          console.log(error);
        });
      },
  },
  watch: {
    moneyAsked: {
        deep: true,
        handler(){
          this.getFixerConversion();
        }
    }
},
  mounted(){
    this.getFixerConversion();
    }
  }
</script>

<style scoped>

</style>