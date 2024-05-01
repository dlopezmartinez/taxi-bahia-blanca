<!-- eslint-disable no-unused-vars -->
<script setup>
import PhoneIcon from './components/PhoneIcon.vue'
import WhatsappIcon from './components/WhatsappIcon.vue'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Navigation, Pagination, Slide } from 'vue3-carousel'
import { ref, onMounted } from 'vue'
const slides = [
  {
    img: getImageUrl('slide1')
  },
  {
    img: getImageUrl('slide2')
  },
  {
    img: getImageUrl('slide3')
  }
]

function getImageUrl(name, extension = 'jpeg') {
  return new URL(`/src/imgs/${name}.${extension}`, import.meta.url).href
}

const viajes = ref(0)
const pasajeros = ref(0)
const localidades = ref(0)
const kilometros = ref(300)

const doCounter = (refConst, max, tick = 10) => {
  const interval = setInterval(() => {
    refConst.value = refConst.value + 1
    if (refConst.value >= max) {
      clearInterval(interval)
    }
  }, tick)
}

onMounted(() => {
  doCounter(viajes, 300, 5)
  doCounter(pasajeros, 30)
  doCounter(localidades, 30)
  doCounter(kilometros, 1000, 1)
})
</script>

<template>
  <header>
    <img :src="getImageUrl('taxi', 'png')" alt="/src/imgs/noimage.png" />
    <h1>Taxi Bahia Blanca</h1>
  </header>

  <main>
    <article class="about-me">
      <section class="about-me--description">
        <div class="description-container">
          <h2>Tu taxi de confianza en cada viaje</h2>
          <p>
            Descubrí la experiencia y seguridad que solo una taxista con años de trayectoria puede
            ofrecerte. Desde viajes cortos hasta largas distancias, siempre te llevaremos con
            cuidado y puntualidad.
          </p>
          <p>¡Confía en nosotros para tu próximo viaje!</p>
        </div>
      </section>
      <section class="about-me--info">
        <p>Pulsa para contactarme por donde prefieras</p>
        <h3>
          <a href="tel:633182123" aria-label="Telefono de contacto"
            >Telefono: 633182123 <PhoneIcon style="margin-left: auto"
          /></a>
        </h3>
        <h3>
          <a
            href="https://wa.me/633182123?text=Hola!, Necesito un viaje."
            aria-label="Whatsapp de contacto"
            target="_blank"
            >Contacta por whatsapp<WhatsappIcon style="margin-left: auto"
          /></a>
        </h3>
      </section>
    </article>

    <article class="carousel--wrapper">
      <h2>Nuestro taxi</h2>
      <h3>Excelencia en movimiento</h3>
      <Carousel :items-to-show="2" :wrap-around="true">
        <slide v-for="slide in slides" :key="slide">
          <div class="carousel-slide--container">
            <img class="carousel-photo" :src="slide.img" alt="/src/imgs/noimage.png" />
            <p>{{ slide.text }}</p>
          </div>
        </slide>
      </Carousel>
      <p>
        Descubrí nuestro impecable taxi, donde la calidad y la limpieza se fusionan para ofrecerte
        un viaje confortable y seguro. Cuidamos cada detalle para garantizarte una experiencia
        inigualable.
      </p>
    </article>
    <article class="numbers">
      <div class="numbers--col">
        <p class="--counter">+{{ viajes }}</p>
        <p class="--description">Viajes realizados</p>
      </div>
      <div class="numbers--col">
        <p class="--counter">{{ pasajeros }}</p>
        <p class="--description">Pasajeros fijos</p>
      </div>
      <div class="numbers--col">
        <p class="--counter">{{ localidades }}</p>
        <p class="--description">Localidades con las que trabajamos</p>
      </div>
      <div class="numbers--col">
        <p class="--counter">{{ kilometros }}K</p>
        <p class="--description">Viaje más largo en kilometros</p>
      </div>
    </article>
  </main>
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
  padding: 10px;
  background-color: var(--color-header);

  img {
    width: 40px;
    height: 40px;
  }
}
.about-me {
  position: relative;
  display: flex;
  width: 100%;
  background: var(--color-main);
}

.about-me--description {
  flex: 2;
  display: flex;
  justify-content: center;
  height: 400px;
}

@media screen and (max-width: 1000px) {
  .about-me--description {
    height: 250px;
  }
}

@media screen and (max-width: 1000px) and (orientation: landscape) {
  .about-me--description {
    height: 250px;
  }
}

.description-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  height: 100%;
  width: 90%;
  padding: 20px 0px;
}

.about-me--container {
  flex: 1;
}

.--photo {
  position: absolute;
  bottom: 0;
  right: 5vw;
  width: 80%;
  height: 400px;
  max-width: 70vw;
}

.about-me--info {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  color: #183372;
  position: absolute;
  bottom: -75px;
  left: 12.5%;
  background: #f4f4f4;
  border-radius: 20px;
  width: 75vw;
  padding: 10px 0px;

  a {
    display: inline-flex;
    align-items: center;
    gap: 20px;
  }

  --color-icon: #183372;
}

.carousel--wrapper {
  margin: auto;
  width: 90%;
  margin-top: 100px;
  padding-bottom: 50px;

  color: #183372;
  display: flex;
  flex-direction: column;
  gap: 20px;
  text-align: center;
}

.carousel-slide--container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.carousel-photo {
  width: 95%;
  max-height: 700px;
  border-radius: 20px;
}

.carousel__pagination-button {
  min-width: 48px;
  min-height: 48px;
}

.numbers {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  place-items: center;
  margin: auto;
  width: 80%;
  color: #183372;
  padding-bottom: 50px;
}

.numbers--col {
  max-width: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.--counter {
  font-size: 64px;
  font-weight: 900;
}

.--description {
  text-align: center;
  text-wrap: wrap;
}
</style>
