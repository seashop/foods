<template>
  <div class="tabbar">
    <template v-for="(item, index) in tab" :key="item.id">
      <router-link :to="{path: item.path}">
        <el-badge :value="totalCount" :max="99" type="danger" v-if="item.id == 3">
          <img :src="num==item.id?item.imgUrl2:item.imgUrl" alt="">
        </el-badge>
        <template v-else>
          <img :src="num==item.id?item.imgUrl2:item.imgUrl" alt="">
        </template>
      </router-link>
    </template>
  </div>
</template>

<script setup lang="ts">
import cartStore from "@/store/cartStore"
import { computed, ref, watch } from "vue"
import { useRoute } from "vue-router"

const route = useRoute()
const cart = cartStore()

const totalCount = cart.cTotalCount
const num = ref(1)
const tab = ref([
  {
    id: 1,
    path: "/",
    imgUrl: "/static/img/home.png",
    imgUrl2: "/static/img/home2.png",
  },
  {
    id: 2,
    path: "/category/1",
    imgUrl: "/static/img/category.png",
    imgUrl2: "/static/img/category2.png",
  },
  {
    id: 3,
    path: "/cart",
    imgUrl: "/static/img/cart.png",
    imgUrl2: "/static/img/cart2.png",
  },
  {
    id: 4,
    path: "/info",
    imgUrl: "/static/img/my.png",
    imgUrl2: "/static/img/my2.png",
  },
])

watch(route, val => {
  let data= tab.value.find(item => item.path == val.path)
  if (data) {
    num.value = data.id
  }
}, { immediate: true })

</script>

<style lang="scss" scoped>

.tabbar {
  height: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
    
  a {
    width: 100%;
    height: 100%;
    display: grid;
    img, .el-badge {
      place-self: center;
      width: 27px;
      height: 27px;
    }
  }
}
.router-link-active {
  color: red;
}

</style>