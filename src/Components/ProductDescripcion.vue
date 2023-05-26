<template>
    <ion-page>
      <ion-content class="ion-padding">
        <div class="product-detail">
           
          <div class="image-container">
            <img :src="productos.imagenArchivo" :alt="productos.nombre">
          </div>
          <div class="product-info">
             <ion-title>{{ productos.nombre }}</ion-title>
            <p class="description">{{ productos.description }}</p>
            <p class="summary">{{ productos.resumen }}</p>
            <p class="price">$ {{ productos.precio }}</p>
          </div>
        </div>
      </ion-content>
    </ion-page>
  </template>
  
  <script>
  import axios from 'axios';
  import { IonPage,IonContent,IonHeader,IonToolbar,IonTitle } from '@ionic/vue';
  export default {
    name: 'ProductDetail',
    data() {
      return {
        
        productos: [],
      };
    },
    components:{
        IonPage,IonContent,IonHeader,IonToolbar,IonTitle
    },
    methods:{
    
        },
    mounted(){
            const id = this.$route.params.id;
            console.log(id)
            axios.get('https://localhost:44318/api/v1/Catalog'+id)
      .then(response => {
        this.productos = response.data;
        console.log(this.productos)
      })
      .catch(error => {
        console.error(error);
      });
        }

  };
  </script>
  
  <style scoped>
  .product-detail {
    display: flex;
    align-items: center;
  }
  
  .image-container {
    width: 200px;
    height: 200px;
    margin-right: 20px;
  }
  
  .product-info {
    flex-grow: 1;
  }
  
  .description {
    font-weight: bold;
  }
  
  .summary {
    margin-top: 10px;
  }
  
  .price {
    margin-top: 20px;
    font-size: 18px;
    font-weight: bold;
  }
  </style>