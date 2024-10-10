<template>
  <f7-page name="home">
    <!-- Top Navbar -->
    <f7-navbar large :sliding="false">
      <f7-nav-left>
        <f7-link icon-ios="f7:menu" icon-md="material:menu" panel-open="left"></f7-link>
      </f7-nav-left>
      <f7-nav-title-large>租屋懶人包</f7-nav-title-large>
    </f7-navbar>

    <!-- Page content-->
    <f7-block v-for="item in rentData" strong inset>
      <f7-block-title>{{ item.title }}</f7-block-title>
      <swiper-container :pagination="true" class="demo-swiper-multiple" :space-between="12">
        <swiper-slide v-for="img in item.images">
          <img :src="img" :alt="item.title" loading="lazy">
        </swiper-slide>
      </swiper-container>
      <div :class="$style.info">
        <span>{{ item.address }}</span>
        <span>{{ item.area }}</span>
        <f7-link :href="item.link" :external="true" target="_blank">連結</f7-link>
      </div>
      <p :class="$style.price">${{ item.price }}</p>
    </f7-block>

  </f7-page>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import axios from 'axios';
interface I591NormalRes {
  "title": string
  "price": string
  "address": string
  "floor": string
  "area": string
  "images": string[]
  "link": string
}
let rentData = ref<I591NormalRes[]>([])
axios.get('http://localhost:5500/temp/591normal.json').then(res => {
  rentData.value = res.data
})
</script>

<style lang="css" module>
.info {
  display: flex;
  gap: 12px;
}
.price {
  text-align: right;
  font-size: 24px;
  color: red;
  margin: 4px 0;
}
</style>