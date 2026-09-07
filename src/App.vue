<script setup lang="ts">
import { ref } from 'vue'
import compassIcon from './assets/brujula.png'
import startIcon from './assets/start.png'
import sheepIcon from './assets/sheep_icon.jpg'
import sheepTitle from './assets/Sheeptitulo.png'
import minecraftIcon from './assets/minecraft_icon.png'
import minecraftTitle from './assets/minecrafticon.png'
import nomansIcon from './assets/nomans_icon.png'
import helldiversIcon from './assets/Helldivers_icon.jpg'
import helldiversTitle from './assets/helldiverstitulo (2).png'
import nomansTitle from './assets/nomanstitulo.png'

const activeItem = ref('Inicio')
const activeVideo = ref(0)
const carouselTrack = ref<HTMLElement | null>(null)
const activeMinecraftVideo = ref(0)
const minecraftCarouselTrack = ref<HTMLElement | null>(null)
const activeNomansVideo = ref(0)
const nomansCarouselTrack = ref<HTMLElement | null>(null)
const activeHelldiversVideo = ref(0)
const helldiversCarouselTrack = ref<HTMLElement | null>(null)

const videos = [
  { title: 'Sheep Raider - Video principal', url: 'https://www.youtube.com/embed/b_Gjvwz62h0' },
  { title: 'Sheep Raider - Video 2', url: 'https://www.youtube.com/embed/sRWAPFxWmRo?si=MAUDvWPURVxm61Bo' },
  { title: 'Sheep Raider - Video 3', url: 'https://www.youtube.com/embed/JabsdYRGwHg?si=aoTJWAsv8kjOnNaj' },
]

const minecraftVideos = [
  { title: 'Minecraft - Video principal', url: 'https://www.youtube.com/embed/MmB9b5njVbA' },
  { title: 'Minecraft - Video 2', url: 'https://www.youtube.com/embed/KbnqaIFth70?si=7pAWZOtxboAs-xiM' },
  { title: 'Minecraft - Video 3', url: 'https://www.youtube.com/embed/oM9fUlGET-w?si=FloY-dCD3yYf3Lor' },
]

const nomansVideos = [
  { title: 'No Man\'s Sky - Video principal', url: 'https://www.youtube.com/embed/c-KoLySxccY?si=EJm8QJXM0bEsXzJs' },
  { title: 'No Man\'s Sky - Video 2', url: 'https://www.youtube.com/embed/GqPTCrIl2BU?si=x7sl5uuydspgcdzk' },
  { title: 'No Man\'s Sky - Video 3', url: 'https://www.youtube.com/embed/HJEJe8HMsY4?si=UTdYQrhbPle6xoXo' },
]

const helldiversVideos = [
  { title: 'Helldivers 2 - Video principal', url: 'https://www.youtube.com/embed/3DJCLVCirQE?si=aPOhvBChD0WUTYhp' },
  { title: 'Helldivers 2 - Video 2', url: 'https://www.youtube.com/embed/2O_9hwQ8jLw?si=QkHJadmHaeIQ27BU' },
  { title: 'Helldivers 2 - Video 3', url: 'https://www.youtube.com/embed/_2Oi8-ISOu4?si=TUir7hjXGDEWhZfg' },
]

const menuItems = [
  { label: 'Inicio', target: 'inicio' },
  { label: 'Sheep Raider', target: 'Sheep Raider' },
  { label: 'Minecraft', target: 'Minecraft' },
{label: 'No mans sky', target: 'No mans sky'},
{label: 'helldivers 2', target: 'helldivers 2'},
  { label: 'jugar', target: 'jugar' },
  { label: 'Ajustes', target: 'ajustes' },
]

function goToSection(item: (typeof menuItems)[number]) {
  activeItem.value = item.label
  document.getElementById(item.target)?.scrollIntoView({ behavior: 'smooth' })
}

function scrollToVideo(index: number) {
  const track = carouselTrack.value
  if (!track) return

  activeVideo.value = index
  track.scrollTo({ left: index * track.clientWidth, behavior: 'smooth' })
}

function updateActiveVideo() {
  const track = carouselTrack.value
  if (!track || !track.clientWidth) return

  activeVideo.value = Math.round(track.scrollLeft / track.clientWidth)
}

function scrollToMinecraftVideo(index: number) {
  const track = minecraftCarouselTrack.value
  if (!track) return

  activeMinecraftVideo.value = index
  track.scrollTo({ left: index * track.clientWidth, behavior: 'smooth' })
}

function updateActiveMinecraftVideo() {
  const track = minecraftCarouselTrack.value
  if (!track || !track.clientWidth) return

  activeMinecraftVideo.value = Math.round(track.scrollLeft / track.clientWidth)
}

function scrollToNomansVideo(index: number) {
  const track = nomansCarouselTrack.value
  if (!track) return

  activeNomansVideo.value = index
  track.scrollTo({ left: index * track.clientWidth, behavior: 'smooth' })
}

function updateActiveNomansVideo() {
  const track = nomansCarouselTrack.value
  if (!track || !track.clientWidth) return

  activeNomansVideo.value = Math.round(track.scrollLeft / track.clientWidth)
}

function scrollToHelldiversVideo(index: number) {
  const track = helldiversCarouselTrack.value
  if (!track) return

  activeHelldiversVideo.value = index
  track.scrollTo({ left: index * track.clientWidth, behavior: 'smooth' })
}

function updateActiveHelldiversVideo() {
  const track = helldiversCarouselTrack.value
  if (!track || !track.clientWidth) return

  activeHelldiversVideo.value = Math.round(track.scrollLeft / track.clientWidth)
}
</script>

<template>
  <div class="app-shell">
    <aside class="sidebar" aria-label="Menu principal">
      <div class="brand">
        <span class="brand-mark">
          <img :src="compassIcon" alt="Brujula" />
        </span>
        <span>Exploracion</span>
      </div>

      <nav class="menu">
        <button
          v-for="item in menuItems"
          :key="item.target"
          class="menu-item"
          :class="{ active: activeItem === item.label }"
          type="button"
          @click="goToSection(item)"
        >
          <img
            v-if="item.label === 'Inicio'"
            class="menu-start-image"
            :src="startIcon"
            alt="Inicio"
          />
          <img
            v-else-if="item.label === 'Sheep Raider'"
            class="menu-dot menu-image"
            :src="sheepIcon"
            alt=""
            aria-hidden="true"
          />
          <img
            v-else-if="item.label === 'Minecraft'"
            class="menu-dot menu-image"
            :src="minecraftIcon"
            alt=""
            aria-hidden="true"
          />
          <img
            v-else-if="item.label === 'No mans sky'"
            class="menu-dot menu-image"
            :src="nomansIcon"
            alt=""
            aria-hidden="true"
          />
          <img
            v-else-if="item.label === 'helldivers 2'"
            class="menu-dot menu-image"
            :src="helldiversIcon"
            alt=""
            aria-hidden="true"
          />
          <span v-else class="menu-dot" aria-hidden="true"></span>
          <span v-if="item.label !== 'Inicio'">{{ item.label }}</span>
        </button>
      </nav>

      <p class="sidebar-footer">Crreado por Alpizar</p>
    </aside>

    <main class="content">
      <section id="inicio" class="page-section intro-section">
        <p class="eyebrow">{{ activeItem }}</p>
        <h1>Mis juegos favoritos</h1>
        <p>Siempre he creído que explorar en un videojuego no es solo presionar "avanzar" y ver qué hay más adelante; es la forma en que el mundo se comunica contigo. No se siente igual caminar con cautela por un cañón colorido tratando de burlar a un perro pastor, que adentrarse a ciegas en una cueva infinita en busca de minerales, navegar por la soledad silenciosa de una galaxia desconocida o correr contra el tiempo en un planeta hostil bajo el fuego enemigo. </p>
        <p>La ambientación y el tono de cada juego transforman por completo el acto de explorar: a veces es un rompecabezas de astucia, a veces un ejercicio contemplativo y, en otras, un descenso caótico donde la curiosidad se paga con la vida. En este espacio reuní algunos de mis juegos favoritos para analizar cómo cada uno convierte el viaje en una experiencia completamente distinta.</p>
      </section>

      <section id="Sheep Raider" class="page-section sheep-section">
        <p class="eyebrow">Juego 1</p>
        <img class="section-title-image" :src="sheepTitle" alt="Sheep Raider" />
        <p>Si me preguntan por las joyas más subestimadas de la PS1, mi mente viaja inmediatamente a Sheep Raider (o Sheep, Dog 'n' Wolf, como lo conocimos muchos). Más allá de las risas y la genial adaptación del universo de los Looney Tunes, lo que realmente me atrapó de este título fue algo que no esperaba encontrar en un juego de sigilo: su brillante y gratificante sentido de la exploración.</p>
        <p>Desviarte del camino principal te llevaba a descubrir cuevas ocultas, repisas secretas para evitar la vista de Sam, o esos esquivos relojes de bonificación que te exigían dominar el entorno. El mapa entero es tu herramienta; descubrir cómo un simple arbusto, una corriente de agua o incluso una máquina del tiempo encajaban en tu loco plan de robo, se sentía como una victoria inmensamente personal.</p>
        <div class="video-carousel" aria-label="Videos de Sheep Raider">
          <div
            ref="carouselTrack"
            class="video-track"
            @scroll="updateActiveVideo"
          >
            <article v-for="video in videos" :key="video.url" class="video-slide">
              <iframe
                :src="video.url"
                :title="video.title"
                loading="lazy"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                allowfullscreen
              ></iframe>
            </article>
          </div>

          <div class="carousel-controls">
            <button
              type="button"
              aria-label="Video anterior"
              :disabled="activeVideo === 0"
              @click="scrollToVideo(activeVideo - 1)"
            >
              &#8592;
            </button>
            <div class="carousel-dots" aria-label="Seleccionar video">
              <button
                v-for="(_, index) in videos"
                :key="index"
                type="button"
                :class="{ selected: activeVideo === index }"
                :aria-label="`Ver video ${index + 1}`"
                :aria-current="activeVideo === index ? 'true' : undefined"
                @click="scrollToVideo(index)"
              ></button>
            </div>
            <button
              type="button"
              aria-label="Siguiente video"
              :disabled="activeVideo === videos.length - 1"
              @click="scrollToVideo(activeVideo + 1)"
            >
              &#8594;
            </button>
          </div>
        </div>
      </section>
      

      <section id="Minecraft" class="page-section minecraft-section">
        <p class="eyebrow">Juego 2</p>
        <img class="section-title-image" :src="minecraftTitle" alt="Minecraft" />
        <p>Si hay un juego que redefinió para siempre lo que significa perderse en un mundo virtual, ese es Minecraft. Más allá de la construcción con bloques y el crafting, lo que verdaderamente atrapa de este título es su inagotable y mágica capacidad de exploración.</p>
        <p>En Minecraft, la exploración no es una simple tarea secundaria; es el motor que impulsa toda tu aventura. El momento en que apareces por primera vez en un mundo generado de forma procedimental, completamente desconocido y sin un mapa que te diga a dónde ir, se siente una mezcla perfecta de vulnerabilidad y absoluta libertad.</p>
        <div class="video-carousel minecraft-carousel" aria-label="Videos de Minecraft">
        <div
          ref="minecraftCarouselTrack"
          class="video-track"
          @scroll="updateActiveMinecraftVideo"
        >
          <article v-for="video in minecraftVideos" :key="video.url" class="video-slide">
            <iframe
              :src="video.url"
              :title="video.title"
              loading="lazy"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
              allowfullscreen
            ></iframe>
          </article>
        </div>

        <div class="carousel-controls">
          <button
            type="button"
            aria-label="Video anterior de Minecraft"
            :disabled="activeMinecraftVideo === 0"
            @click="scrollToMinecraftVideo(activeMinecraftVideo - 1)"
          >
            &#8592;
          </button>
          <div class="carousel-dots" aria-label="Seleccionar video de Minecraft">
            <button
              v-for="(_, index) in minecraftVideos"
              :key="index"
              type="button"
              :class="{ selected: activeMinecraftVideo === index }"
              :aria-label="`Ver video de Minecraft ${index + 1}`"
              :aria-current="activeMinecraftVideo === index ? 'true' : undefined"
              @click="scrollToMinecraftVideo(index)"
            ></button>
          </div>
          <button
            type="button"
            aria-label="Siguiente video de Minecraft"
            :disabled="activeMinecraftVideo === minecraftVideos.length - 1"
            @click="scrollToMinecraftVideo(activeMinecraftVideo + 1)"
          >
            &#8594;
          </button>
        </div>
      </div>
      <div>
        
      </div>
      </section>
      <section id="No mans sky" class="page-section nomans-section">
        <p class="eyebrow">Juego 3</p>
        <img class="section-title-image" :src="nomansTitle" alt="No Man's Sky" />
        <p>Si Minecraft me enseñó lo que es perderse en un mapa infinito, No Man's Sky llevó esa sensación a una escala literalmente cósmica. Si tuviera que definirlo en una sola palabra, sería inmensidad. Para mí, este juego es la máxima expresión de lo que significa ser un explorador en el sentido más puro y romántico del término.</p>
        <div class="video-carousel nomans-carousel" aria-label="Videos de No Man's Sky">
          <div
            ref="nomansCarouselTrack"
            class="video-track"
            @scroll="updateActiveNomansVideo"
          >
            <article v-for="video in nomansVideos" :key="video.url" class="video-slide">
              <iframe
                :src="video.url"
                :title="video.title"
                loading="lazy"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                allowfullscreen
              ></iframe>
            </article>
          </div>

          <div class="carousel-controls">
            <button
              type="button"
              aria-label="Video anterior de No Man's Sky"
              :disabled="activeNomansVideo === 0"
              @click="scrollToNomansVideo(activeNomansVideo - 1)"
            >
              &#8592;
            </button>
            <div class="carousel-dots" aria-label="Seleccionar video de No Man's Sky">
              <button
                v-for="(_, index) in nomansVideos"
                :key="index"
                type="button"
                :class="{ selected: activeNomansVideo === index }"
                :aria-label="`Ver video de No Man's Sky ${index + 1}`"
                :aria-current="activeNomansVideo === index ? 'true' : undefined"
                @click="scrollToNomansVideo(index)"
              ></button>
            </div>
            <button
              type="button"
              aria-label="Siguiente video de No Man's Sky"
              :disabled="activeNomansVideo === nomansVideos.length - 1"
              @click="scrollToNomansVideo(activeNomansVideo + 1)"
            >
              &#8594;
            </button>
          </div>
        </div>
      </section>

      <section id="helldivers 2" class="page-section helldivers-section">
        <p class="eyebrow">Juego 4</p>
        <img class="section-title-image" :src="helldiversTitle" alt="Helldivers 2" />
        <p>A primera vista, podrías pensar que un shooter cooperativo centrado en exterminar bichos gigantes y autómatas no tiene mucho margen para la exploración, pero la realidad es otra. En Helldivers 2, explorar el mapa no es un lujo: es una necesidad de supervivencia.</p>
        <p>Para mí, la exploración en Helldivers 2 funciona porque nunca estás a salvo. Ese contraste entre la calma relativa de escanear el horizonte buscando un punto de interés y el caos absoluto cuando accidentalmente pisas una patrulla enemiga es la razón por la que siempre quiero bajar a un planeta más en nombre de la Democracia.</p>
        <div class="video-carousel helldivers-carousel" aria-label="Videos de Helldivers 2">
          <div
            ref="helldiversCarouselTrack"
            class="video-track"
            @scroll="updateActiveHelldiversVideo"
          >
            <article v-for="video in helldiversVideos" :key="video.url" class="video-slide">
              <iframe
                :src="video.url"
                :title="video.title"
                loading="lazy"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                allowfullscreen
              ></iframe>
            </article>
          </div>

          <div class="carousel-controls">
            <button
              type="button"
              aria-label="Video anterior de Helldivers 2"
              :disabled="activeHelldiversVideo === 0"
              @click="scrollToHelldiversVideo(activeHelldiversVideo - 1)"
            >
              &#8592;
            </button>
            <div class="carousel-dots" aria-label="Seleccionar video de Helldivers 2">
              <button
                v-for="(_, index) in helldiversVideos"
                :key="index"
                type="button"
                :class="{ selected: activeHelldiversVideo === index }"
                :aria-label="`Ver video de Helldivers 2 ${index + 1}`"
                :aria-current="activeHelldiversVideo === index ? 'true' : undefined"
                @click="scrollToHelldiversVideo(index)"
              ></button>
            </div>
            <button
              type="button"
              aria-label="Siguiente video de Helldivers 2"
              :disabled="activeHelldiversVideo === helldiversVideos.length - 1"
              @click="scrollToHelldiversVideo(activeHelldiversVideo + 1)"
            >
              &#8594;
            </button>
          </div>
        </div>
      </section>

      <section id="ajustes" class="page-section info-section">
        <p class="eyebrow">Preferencias</p>
        <h2>Mini Juego</h2>
        <p>Los RPGs de texto también conocidos como ficción interactiva (IF) o los clásicos juegos de mazmorras como los MUDs (Multi-User Dungeons)— son prácticamente los abuelos de todo el diseño de juegos y exploración que vemos hoy en día.</p>
      </section>

      <section id="jugar" class="page-section info-section rpg-section">
        <p class="eyebrow">Guia</p>
        

      </section>

      
    </main>
  </div>
</template>

<style scoped>
.app-shell {
  display: flex;
  min-height: 100svh;
  background: #0b0b09;
  color: #27251f;
}

.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  display: flex;
  width: 230px;
  flex-direction: column;
  min-height: 100svh;
  padding: 28px 18px;
  box-sizing: border-box;
  background: #232c26;
  color: #f5f1e8;
  box-shadow: 4px 0 18px rgba(35, 44, 38, 0.18);
}

.brand {
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 0 10px 54px;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.8px;
  text-transform: uppercase;
}

.brand-mark {
  display: grid;
  width: 38px;
  height: 38px;
  place-items: center;
  overflow: hidden;
  border: 1px solid #c9a86a;
  color: #c9a86a;
  font-size: 11px;
  letter-spacing: 0;
}

.brand-mark img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.menu {
  display: grid;
  gap: 8px;
}

.menu-item {
  display: flex;
  align-items: center;
  gap: 12px;
  width: 100%;
  padding: 13px 12px;
  border: 0;
  border-left: 2px solid transparent;
  background: transparent;
  color: #bdc5bb;
  font: inherit;
  font-size: 15px;
  text-align: left;
  cursor: pointer;
  transition: background 0.2s ease, color 0.2s ease, border-color 0.2s ease;
}

.menu-item:hover,
.menu-item.active {
  border-left-color: #c9a86a;
  background: #304036;
  color: #fffaf0;
}

.menu-dot {
  width: 7px;
  height: 7px;
  border: 1px solid currentColor;
  border-radius: 50%;
}

.menu-image {
  width: 22px;
  height: 22px;
  flex: 0 0 22px;
  border: 0;
  border-radius: 50%;
  object-fit: cover;
}

.menu-start-image {
  display: block;
  width: 64px;
  height: 64px;
  margin-inline: auto;
  object-fit: contain;
}

.active .menu-dot {
  background: #c9a86a;
  border-color: #c9a86a;
}

.menu-item.active .menu-image {
  border: 1px solid #c9a86a;
}

.sidebar-footer {
  margin: auto 10px 0;
  color: #7f8b80;
  font-size: 12px;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.content {
  flex: 1;
  min-width: 0;
  margin-left: 230px;
  padding: 42px clamp(24px, 6vw, 88px) 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

.page-section {
  min-height: 100svh;
  padding: 28px 0 80px;
  box-sizing: border-box;
  scroll-margin-top: 24px;
}

.intro-section {
  padding-top: 0;
}

.intro-section p:not(.eyebrow) {
  margin-inline: auto;
  text-align: center;
}

.page-section h2 {
  margin-bottom: 18px;
  color: #27251f;
}

.section-title-image {
  display: block;
  width: min(100%, 260px);
  height: 96px;
  margin: 0 auto 18px;
  object-fit: contain;
}

.minecraft-section {
  margin-inline: calc(-1 * clamp(24px, 6vw, 88px));
  padding-inline: clamp(24px, 6vw, 88px);
  background-image:
    linear-gradient(
      to bottom,
      rgba(11, 11, 9, 0) 0%,
      rgba(11, 11, 9, 0.18) 58%,
      #0b0b09 100%
    ),
    url('./assets/minecraft.jpg');
  background-position: center top;
  background-repeat: no-repeat;
  background-size: cover;
}

.nomans-section {
  background-image:
    linear-gradient(
      to bottom,
      rgba(11, 11, 9, 0) 0%,
      rgba(11, 11, 9, 0.18) 58%,
      #0b0b09 100%
    ),
    url('./assets/nomans.png');
  background-position: center top;
  background-repeat: no-repeat;
  background-size: cover;
}

.helldivers-section {
  background-image:
    linear-gradient(
      to bottom,
      rgba(11, 11, 9, 0) 0%,
      rgba(11, 11, 9, 0.18) 58%,
      #0b0b09 100%
    ),
    url('./assets/Helldivers.jpg');
  background-position: center 68%;
  background-repeat: no-repeat;
  background-size: cover;
}

.sheep-section,
.minecraft-section,
.nomans-section,
.helldivers-section {
  margin-inline: calc(-1 * clamp(24px, 6vw, 88px));
  padding-inline: clamp(24px, 6vw, 88px);
}

.sheep-section {
  background-image:
    linear-gradient(
      to bottom,
      rgba(11, 11, 9, 0) 0%,
      rgba(11, 11, 9, 0.28) 42%,
      rgba(11, 11, 9, 0.78) 72%,
      #0b0b09 100%
    ),
    url('./assets/sheep.jpg');
  background-position: center top;
  background-repeat: no-repeat;
  background-size: cover;
}

.video-carousel {
  width: min(100%, 760px);
  margin-inline: auto;
}

.sheep-section p:not(.eyebrow),
.minecraft-section p:not(.eyebrow),
.nomans-section p:not(.eyebrow),
.helldivers-section p:not(.eyebrow) {
  margin-inline: auto;
}

.video-track {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  overscroll-behavior-x: contain;
  border: 1px solid #d9d0bd;
  background: #232c26;
}

.video-track::-webkit-scrollbar {
  display: none;
}

.video-slide {
  flex: 0 0 100%;
  scroll-snap-align: start;
  aspect-ratio: 16 / 9;
}

.video-slide iframe {
  display: block;
  width: 100%;
  height: 100%;
  border: 0;
}

.carousel-controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 14px;
}

.carousel-controls > button,
.carousel-dots button {
  border: 1px solid #c9a86a;
  background: transparent;
  color: #615c51;
  cursor: pointer;
}

.carousel-controls > button {
  width: 38px;
  height: 34px;
  font-size: 20px;
  line-height: 1;
}

.carousel-controls button:hover:not(:disabled),
.carousel-controls button:focus-visible {
  background: #c9a86a;
  color: #232c26;
}

.carousel-controls button:focus-visible {
  outline: 2px solid #232c26;
  outline-offset: 3px;
}

.carousel-controls button:disabled {
  cursor: not-allowed;
  opacity: 0.35;
}

.carousel-dots {
  display: flex;
  gap: 8px;
}

.carousel-dots button {
  width: 9px;
  height: 9px;
  padding: 0;
  border-radius: 50%;
}

.carousel-dots button.selected {
  background: #c9a86a;
}

.page-section p:not(.eyebrow) {
  max-width: 620px;
  color: #615c51;
}

.sheep-section p:not(.eyebrow),
.minecraft-section p:not(.eyebrow),
.nomans-section p:not(.eyebrow),
.helldivers-section p:not(.eyebrow) {
  box-sizing: border-box;
  padding: 16px 20px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  background: rgba(0, 0, 0, 0.6);
  color: #FFFFFF;
}

.sheep-section h2 {
  color: #000;
}

.info-section {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.rpg-section {
  background-color: #0b0b09;
  background-image: url('./assets/rpgfondo.jpg');
  background-position: center top;
  background-repeat: no-repeat;
  background-size: min(1100px, calc(100% - 48px)) auto;
}

.eyebrow {
  margin-bottom: 8px;
  color: #9a7740;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.content h1 {
  margin-top: 0;
  color: #27251f;
}

@media (max-width: 700px) {
  .app-shell {
    display: block;
  }

  .sidebar {
    position: static;
    width: auto;
    min-height: auto;
    padding: 16px;
  }

  .brand {
    margin: 0 4px 16px;
  }

  .menu {
    display: flex;
    gap: 4px;
    overflow-x: auto;
  }

  .menu-item {
    flex: 0 0 auto;
    width: auto;
    border-bottom: 2px solid transparent;
    border-left: 0;
  }

  .menu-item:hover,
  .menu-item.active {
    border-bottom-color: #d3c3a9;
    border-left-color: transparent;
  }

  .sidebar-footer {
    display: none;
  }

  .content {
    margin-left: 0;
    padding: 28px 20px 0;
  }

  .sheep-section {
    margin-inline: -20px;
    padding-inline: 20px;
  }

  .minecraft-section {
    margin-inline: -20px;
    padding-inline: 20px;
  }

  .nomans-section {
    margin-inline: -20px;
    padding-inline: 20px;
  }

  .helldivers-section {
    margin-inline: -20px;
    padding-inline: 20px;
  }

  .rpg-section {
    background-size: calc(100% - 32px) auto;
  }
}
</style>
