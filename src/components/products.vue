<template>
  <div class="carrito-icono">
    <i class="fas fa-shopping-cart"></i>
    <div id="carrito">
      <span id="cantidad-productos">0</span>
      <div v-if="this.cantidadProductos != 0">
        <img id="trash" src="https://cdn-icons-png.flaticon.com/512/1214/1214428.png" v-on:click="vaciarCarrito()" />
      </div>
      <img src="https://cdn-icons-png.flaticon.com/512/872/872243.png" />
    </div>

  </div>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div>
    <ul>
      <li v-for="producto in productos" :key="producto.id">
        {{ producto.title }}
        <img :src="producto.image" alt="Imagen del producto">
        <h1>$ {{ producto.price }}</h1>
        <div>
          <button class="add-to-cart-btn" v-on:click="agregarProducto()"><img
              src="https://cdn-icons-png.flaticon.com/512/3523/3523887.png" /></button>
          <button id="show-popup-btn" class="view-more-btn" v-on:click="showDescription(producto.description)"><img
              src="https://cdn-icons-png.flaticon.com/512/570/570978.png" /></button>
          <div id="popup-container">
            <div id="popup">
              <span id="popup-text"></span>
              <button id="close-popup-btn">&times;</button>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>
  
<script>
import axios from 'axios';
export default {
  methods: {
    agregarProducto() {
      this.cantidadProductos++;
      document.getElementById("cantidad-productos").innerHTML = this.cantidadProductos;
    },

    showDescription(text) {
      const showPopupBtn = document.getElementById('show-popup-btn');
      const popupContainer = document.getElementById('popup-container');
      const popupText = document.getElementById('popup-text');
      const closePopupBtn = document.getElementById('close-popup-btn');

      showPopupBtn.addEventListener('click', () => {
        popupText.textContent = text;
        popupContainer.style.display = 'flex';
      });

      closePopupBtn.addEventListener('click', () => {
        popupContainer.style.display = 'none';
      });

    },
    vaciarCarrito() {
      if (confirm('Are you sure to delete your car?')) {
        this.cantidadProductos = 0;
        document.getElementById("cantidad-productos").innerHTML = this.cantidadProductos;
      }

    },

  },
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Products',
  props: {
    //msg: String
  },
  data() {
    return {
      cantidadProductos: 0,
      productos: [],
    }
  },
  mounted() {
    axios.get('https://fakestoreapi.com/products')
      .then(response => {
        this.productos = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  }
}
</script>
  
<style>
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 0;
  margin: 0;
  list-style: none;
  max-width: 100%;
}

li {
  width: calc(20% - 20px);
  height: 550px;
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  transition: transform 0.2s ease-in-out;
  background-color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  /* justify-content: center; */
}

li:hover {
  transform: translateY(-5px);
}

li img {
  display: block;
  max-width: 150px;
  height: auto;
  border-radius: 5px;
}

li h3 {
  margin: 10px 0;
  font-size: 16px;
  font-weight: bold;
  color: #333;
  text-align: center;
}

p {
  margin: 10px 0;
  padding: auto;
  font-size: 14px;
  color: #777;
  text-align: center;
  text-align: justify;
}


.add-to-cart-btn,
.view-more-btn {
  padding: 10px 20px;
  margin-right: 5px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.add-to-cart-btn:hover,
.view-more-btn:hover {
  background-color: #0062cc;
}

.add-to-cart-btn img,
.view-more-btn img {
  max-width: 30px;
}


.carrito-icono {
  position: relative;
  display: inline-block;
}

.carrito-icono i {
  font-size: 24px;
}

.carrito-icono #cantidad-productos {
  position: absolute;
  top: -10px;
  right: -10px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: red;
  color: white;
  font-size: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
}

#carrito {
  position: relative;
  display: inline-block;
}

#cantidad-productos {
  position: absolute;
  top: -10px;
  right: -10px;
  background-color: red;
  color: white;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
}

#carrito img {
  width: 50px;
  height: 50px;
}

.carrito-icono {
  position: fixed;
  top: 0;
  right: 0;
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}


#popup-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
  display: none;
}

#popup {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  max-width: 90%;
  max-height: 90%;
  overflow: auto;
  animation: zoom-in 0.2s ease-out;
}

#popup-text {
  display: block;
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 20px;
  text-align: center;
}

#close-popup-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 1.5rem;
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  transition: all 0.2s ease-out;
}

#close-popup-btn:hover {
  transform: rotate(90deg);
}

@keyframes zoom-in {
  from {
    transform: scale(0);
  }

  to {
    transform: scale(1);
  }
}

#trash {
  max-width: 20px;
  max-height: 20px;
}
</style>
  