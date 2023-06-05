<template>
  <div class="home">

    <section class="py-5 text-center container">
      <div class="row py-lg-5">
        <div class="col-lg-6 col-md-8 mx-auto">
          <h1 class="fw-light">Album example</h1>
          <p class="lead text-muted">Something short and leading about the collection below—its contents, the creator,
            etc. Make it short and sweet, but not too short so folks don’t simply skip over it entirely.</p>
          <p>
            <a href="#" class="btn btn-primary my-2">Main call to action</a>
            <a href="#" class="btn btn-secondary my-2">Secondary action</a>
          </p>
        </div>
      </div>
    </section>

    <div class="album py-5 bg-light">
      <div class="container">
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
          <div class="col" v-for="(item, idx) in state.items" :key="idx">
            {{item}}
            <!--Card에 item 전달을 위해, 즉 props -->
            <Card :item="item"></Card>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import Card from "@/components/Card.vue";
import axios from "axios";
import {reactive} from "vue";

export default {
  name: "Home",
  components: {Card},
  setup() {
    const state = reactive({
      items: [],
    })
    //axios.get : axios해서 get방식으로 가져올꺼야
    //.then((res) => {console.log(res);}) : 그런 다음에 res결과를 받으면 console을 찍어보자
    // axios.get("api/items").then((res) => {
    //   console.log(res);
    //   state.items = res.data;
    // })

    // 위와 같다. 매개변수를 data로 하면 .data를 붙이지 않고도 특정 property값을 바로 꺼낼 수 있다.
    // todo: 그런데, 나는 안 먹혀서 data.data로 값을 줌
    axios.get("api/items").then((data) => {
      state.items = data.data;
    })

    return {state}
  },
}
</script>

<style scoped>

</style>