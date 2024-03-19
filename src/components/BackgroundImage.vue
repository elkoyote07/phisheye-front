<template>
    <div class="background-image">
      <img :src="backgroundImage" alt="Background Image" class="background-image__img">
      <div class="background-image__overlay"></div>
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    name: 'BackgroundImage',
    props: {
      backgroundImage: {
        type: String,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .background-image {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }
  
  .background-image__img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover; /* Ajusta la imagen para que cubra todo el contenedor */
    filter: blur(10px); /* Aplica el efecto de desenfoque */
  }
  
  .background-image__overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /* Ajusta el color y la opacidad del fondo */
  }
  </style>
  