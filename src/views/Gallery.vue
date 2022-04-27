<template>
  <div id="galleryContainer">
    <Card v-for="(item,index) in $store.state.galleryStore" @click="card(index)" :key="index" :item="item"/>
    <div id="gallerySliderContainer" :style="{display:galleryİnfo.galleryDisplay}">
      <div id="gallerySliderCap">
        <img :src="galleryİnfo.galleryImg" alt="No Picturek!">
        <div id="galleryNextBack">
          <button @click="galleryBack"><fa icon="angle-left"></fa></button>
          <button @click="galleryNext"><fa icon="angle-right"></fa></button>
        </div>
        <div id="galleryQuit" @click="galleryQuit"><fa icon="xmark"></fa></div>
        <div id="galleryNumber">{{galleryİnfo.galleryNumber+1}}</div>
        <div id="galleryBackZoom" @mousemove="galleryZoomMove" @mouseleave="galleryZoomLeave"></div>
        <div id="galleryZoom" :style="{
          left:`${galleryİnfo.galleryZoomLeft - 75}px`,
          top:`${galleryİnfo.galleryZoomTop - 75}px`,
          backgroundPositionX:`-${galleryİnfo.galleryZoomLeft}px`,
          backgroundPositionY:`-${galleryİnfo.galleryZoomTop}px`,
          backgroundImage:`url(${galleryİnfo.galleryImg})`,
          backgroundSize:galleryİnfo.galleryImgSize,
          display:galleryİnfo.galleryZoomDiplay
          }"></div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from '../components/Card.vue';

export default {
  components:{
    Card
  },
  data() {
    return {
      galleryİnfo : {
        galleryDisplay : 'none',
        galleryImg : '',
        galleryImgSize : '',
        galleryNumber : '',
        galleryZoomLeft : 0,
        galleryZoomTop : 0,
        galleryZoomDiplay : 'none'
      },
    }
  },
  methods: {
    card(e){
      this.galleryİnfo.galleryDisplay = this.galleryİnfo.galleryDisplay == 'none' ? 'flex' : 'none';
      this.galleryİnfo.galleryImg = this.$store.state.galleryStore[e].ımg;
      this.galleryİnfo.galleryImgSize = this.$store.state.galleryStore[e].size;
      this.galleryİnfo.galleryNumber = e;
    },
    galleryQuit(){
      this.galleryİnfo.galleryDisplay = this.galleryİnfo.galleryDisplay == 'none' ? 'flex' : 'none';
    },
    galleryBack(){
      this.galleryİnfo.galleryNumber = this.galleryİnfo.galleryNumber == 0 ? 0 : this.galleryİnfo.galleryNumber - 1;
      this.galleryİnfo.galleryImg = this.$store.state.galleryStore[this.galleryİnfo.galleryNumber].ımg;
      this.galleryİnfo.galleryImgSize = this.$store.state.galleryStore[this.galleryİnfo.galleryNumber].size;
    },
    galleryNext(){
      this.galleryİnfo.galleryNumber = this.galleryİnfo.galleryNumber == this.$store.state.galleryStore.length-1 ? this.$store.state.galleryStore.length-1 : this.galleryİnfo.galleryNumber + 1;
      this.galleryİnfo.galleryImg = this.$store.state.galleryStore[this.galleryİnfo.galleryNumber].ımg;
      this.galleryİnfo.galleryImgSize = this.$store.state.galleryStore[this.galleryİnfo.galleryNumber].size;
    },
    galleryZoomMove(e){
      this.galleryİnfo.galleryZoomDiplay = 'block';
      this.galleryİnfo.galleryZoomLeft = e.offsetX;
      this.galleryİnfo.galleryZoomTop = e.offsetY;
    },
    galleryZoomLeave(){
      this.galleryİnfo.galleryZoomDiplay = 'none';
    }
  },
}
</script>