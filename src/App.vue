<template>
  <IonPage>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
  </IonPage> 
</template>

<script>
import { IonApp, IonRouterOutlet,IonPage } from '@ionic/vue';
export default {
  components:{
    IonApp, IonRouterOutlet, IonPage
  }
}
</script>

<style>

</style>
