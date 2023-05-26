<template>
  <ion-grid>
    <ion-row class="ion-justify-content-center">
      <ion-col size="12" size-xs="6" size-sm="6" size-md="6" size-lg="3" v-for="product in products" :key="product.id">
        <ion-card class="product-card" :class="{ flipped: product.activeCard === 'back' }"
          @click="toggleCardFlip(product)">
          <div class="card-inner">
            <div class="card-front" v-show="product.activeCard === 'front'">
              <img alt="imagen" :src="product.imagenArchivo" class="product-image" />
              <div class="product-content">
                <ion-card-header class="ion-text-center">
                  <ion-card-title class="product-title">{{ product.nombre }}</ion-card-title>
                </ion-card-header>
                <ion-card-content>
                  <div class="product-info">
                    <p><strong>Categoria:</strong> {{ product.categoria }}</p>
                    <p><strong>Resumen:</strong> {{ product.resumen }}</p>
                    <p><strong>Precio:</strong> {{ product.precio }}</p>
                  </div>
                </ion-card-content>
              </div>
            </div>
            <div class="card-back" v-show="product.activeCard === 'back'">
              <div class="product-content">
                <ion-card-content>
                  <div class="product-info">
                    <p><strong>Descripcion:</strong> {{ product.descripcion }}</p>
                  </div>
                </ion-card-content>
              </div>
            </div>
          </div>
        </ion-card>
      </ion-col>
    </ion-row>
  </ion-grid>
</template>

<script>
import { IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonButton, IonIcon } from '@ionic/vue';
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  components: { IonCard, IonCardHeader, IonCardTitle, IonCardContent, IonButton, IonIcon },
  data() {
    return {
      products: [],
    };
  },
  mounted() {

    this.fetchProducts();


  },
  methods: {
    fetchProducts() {
      axios.get('https://localhost:44318/api/v1/Catalog ')
        .then(response => {
          this.products = response.data.map(item => ({
            id: item.id,
            nombre: item.nombre,
            categoria: item.categoria,
            resumen: item.resumen,
            descripcion: item.descripcion,
            imagenArchivo: item.imagenArchivo,
            precio: item.precio,
            activeCard: 'front',
            flipped: true

          }));
          console.log(this.products.nombre)

        })
        .catch(error => {
          console.error(error);
        });
    },


    toggleCardFlip(product) {

      if (product.activeCard === 'front') {
        product.activeCard = 'back';
      } else {
        product.activeCard = 'front';
      }

    },
  },
});
</script>

<style scoped>
.product-card {
  width: 90%;
  height: 500px;
}

.product-image {
  width: 90%;
  height: 200px;
  object-fit: cover;
  margin: 10%;
  border: 2px solid #9efff0;
  border-radius: 5px;
}


.product-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.product-title {
  --background: #000;
  --color: #9efff0;
  font-size: 18px;
  font-weight: bold;
  margin: 10px 0;
}

.product-info {
  text-align: center;
  --background: #000;
  --color: #9efff0;
  font-size: 14px;
  margin-bottom: 10px;
}

.product-details {
  --background: #000;
  --color: #9efff0;
  text-align: center;
  font-size: 14px;
  margin: 10px;
}

.card-inner {
  width: 100%;
  height: 500px;
  transition: transform 0.5s;
  transform-style: preserve-3d;
}

.card-front,
.card-back {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  max-width: 300px;
  margin: 10px auto;
  border: 1px solid #ffffff22;
  background: #000;
  color: #9efff0;
  box-shadow: 0 7px 20px 5px #00000088;
  border-radius: .7rem;
  overflow: hidden;
  backface-visibility: hidden;
  transition: transform 0.5s;

}

.card-front {
  z-index: 2;
  transform: rotateY(0deg);
}

.card-back {
  transform: rotateY(180deg);
}

.flipped .card-inner {
  transform: rotateY(180deg);
}
</style>


