<template>
  <ion-page>
    <ion-header>
        <ion-toolbar>
    <ion-buttons slot:secondary>
        <ion-back-button></ion-back-button>
    </ion-buttons>
    <ion-buttons slot:primary>
      <ion-button id="open-modal" expand="block" fill="outline">
        Edit
        <ion-icon slot:end :icon="create"></ion-icon>
      </ion-button>
    </ion-buttons>
    <ion-title>Detalle</ion-title>
  </ion-toolbar>
  </ion-header>
    <ion-content :fullscreen="true">
      <div>
        <Detalle/>
      </div>

      <!--
        Modal para hacer la edicion del registro
      -->
      <ion-modal ref="modal" trigger="open-modal" @willDismiss="onWillDismiss">
      <ion-header>
        <ion-toolbar>
          <ion-buttons slot:secondary>
            <ion-button @click="cancel()">Cancel</ion-button>
          </ion-buttons>
          <ion-title>Welcome</ion-title>
          <ion-buttons slot:primary>
            <ion-button :strong="true" @click="confirm()">Confirm</ion-button>
          </ion-buttons>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
          <ion-input style="margin-top: 20px;" label="Nombre:" v-model="productos.nombre" label-placement="floating" fill="outline"></ion-input>
          <ion-input style="margin-top: 20px;" label="Categoria:" v-model="productos.categoria" label-placement="floating" fill="outline"></ion-input>
          <ion-input style="margin-top: 20px;" label="Descripcion:" v-model="productos.descripcion" label-placement="floating" :counter="true" maxlength="100" fill="outline"></ion-input>
          <ion-input style="margin-top: 20px;" label="Resumen:" v-model="productos.resumen" label-placement="floating" :counter="true" maxlength="50" fill="outline"></ion-input>
          <ion-input style="margin-top: 20px;" label="Imagen URL:" v-model="productos.imagenArchivo" label-placement="floating" fill="outline"></ion-input>
          <ion-input style="margin-top: 20px;" label="Precio:" v-model="productos.precio" label-placement="floating" fill="outline"></ion-input>
      </ion-content>
    </ion-modal>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from 'axios';
import { IonPage,IonContent,IonTitle,IonToolbar,IonButtons,IonBackButton,IonHeader,IonButton, IonIcon,IonModal,IonItem,
    IonInput,
    IonLabel } from '@ionic/vue';
import Detalle from '../Components/ProductDescripcion.vue';
import { create } from 'ionicons/icons';
export default {
data(){
    return{
        productos:{
          id:"",
          nombre:"",
          categoria:"",
          resumen:"",
          descripcion:"",
          imagenArchivo:"",
          precio:""
        }
    }
    
},
    components:{
    IonPage,IonContent, Detalle,IonTitle,IonToolbar,IonBackButton,IonButtons,IonButton,IonHeader,IonIcon,IonModal,IonItem,
    IonInput,
    IonLabel
    },
    setup() {
      return { create };
    },
    methods:{
        cancel() {
        this.$refs.modal.$el.dismiss(null, 'cancel');
      },
      confirm() {
        this.ActualizarRegistro()
        const name = this.$refs.input.$el.value;
        this.$refs.modal.$el.dismiss(name, 'confirm');
      },
      onWillDismiss(ev) {
  if (ev.detail.role === 'confirm') {
    this.message = 'Hello, ' + ev.detail.data + '!';
  }
},
ActualizarRegistro(){
  axios.put('https://localhost:44350/api/v1/catalog/',this.productos)
      .then(response => {
        console.log(response.data)
      })
      .catch(error => {
        console.error(error);
      });
}
      },
      mounted(){
            const id = this.$route.params.id;
            console.log(id)
            axios.get('https://localhost:44350/api/v1/catalog/'+id)
      .then(response => {
        this.productos = response.data;
        console.log(this.productos)
      })
      .catch(error => {
        console.error(error);
      });
        }
    }

</script>

<style scoped>
ion-toolbar{
    align-items: center;
}
.informacion{
  color:mediumblue;
}

</style>