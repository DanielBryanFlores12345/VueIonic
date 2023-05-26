<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>UTTT SHOP</ion-title>
        <ion-searchbar></ion-searchbar>
        <ion-button  id="open-picker">Categoria</ion-button>
   
        <ion-picker trigger="open-picker" :columns="pickerColumns" :buttons="pickerButtons"></ion-picker>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div>
        <product-card />
      </div>
    </ion-content>
  </ion-page>
</template>
<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonPicker, IonSearchbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import ProductCard from '../Components/ProductCard.vue';

export default defineComponent({
  components: { IonButton, IonPicker, IonContent, IonHeader, IonPage, IonTitle, IonToolbar, ProductCard, IonSearchbar },
  setup() {
    const pickerColumns = [
      {
        name: 'Categorias',
        options: [
          {
            text: 'VideoJuegos',
            value: 'VideoJuegos',
          },
          {
            text: 'Moviles',
            value: 'Moviles',
          },
          {
            text: 'PC',
            value: 'PC',
          },
          {
            text: 'ALL',
            value: 'ALL',
          },
        ],
      },
    ];

    const pickerButtons = [
      {
        text: 'Cancel',
        role: 'cancel',
      },
      {
        text: 'Confirm',
        handler: (value) => {
          window.alert(`You selected: ${value.Categorias.value}`);
        },
      },
    ];

    return { pickerColumns, pickerButtons };
  },
});
</script>

<style scoped>

ion-header {
  background: #000;
  --color: #fff;
}


ion-button{
  --background: #000;
  --color: #9efff0;
  --ripple-color: #ff0000;
}

ion-title {
  text-align: center;
  display: flex;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  border: 2px solid #9efff0;
  border-radius: 5px;
  background-color: #000;
  padding: 8px 16px;
 
}



ion-picker {
  --background: #000;
  color: #fff;
  --border-color: #9efff0;
}

ion-searchbar {
  --background: #000;
  --color: #fff;

  border-radius: 5px;
  background-color: #000;

  display: flex;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  border: 2px solid red;
  border-radius: 5px;
  background-color: #000;
  padding: 8px 16px;

}

</style>
