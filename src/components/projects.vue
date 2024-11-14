<template>
  <main>
    <section id="section1">
      <p>section1</p>
    </section>
    <section id="section2">
      <p>section2</p>
      <div class="box_wrapper">
        <div class="box box1 horizon_box">
          <h1>1</h1>
        </div>
        <div class="box box2 horizon_box">
          <h1>2</h1>
        </div>
        <div class="box box3 horizon_box">
          <h1>3</h1>
        </div>
      </div>
    </section>
    <section id="section6">
      <p>section3</p>
    </section>
    <section id="section7">
      <p>section4</p>
    </section>
  </main>
</template>

<script setup>
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

const main = ref();
let ctx;

onMounted(() => {
  ctx = gsap.context((self) => {
    var $sections = document.querySelectorAll(".horizon_box");
    var tl = gsap.timeline({
      scrollTrigger: {
        trigger: "#section2",
        pin: true,
        scrub: 0.3,
        start: "top top",
        end: "+=3000",
        markers: true,
      },
    });
    tl.to($sections, {
      xPercent: -100,
      duration: 2,
      ease: "none",
      stagger: 3,
    }).to({}, { duration: 1 }); // 스크롤시 약간 정지되는 느낌을 주기
  });
}, main.value); // <- Scope!

onUnmounted(() => {
  ctx.revert(); // <- Easy Cleanup!
});
</script>

<style lang="scss" scoped>
* {
  margin: 0;
}
body {
  margin: 0;
}
section {
  position: relative;
  width: 100%;
  height: 100vh;
}

#section1 {
  background-color: yellowgreen;
  background-image: url("@/assets/section1.png");
  background-size: cover;
  background-repeat: no-repeat;
}

#section2 {
  background: goldenrod;
  overflow: hidden;
  background-image: url("@/assets/section2.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.horizon_box {
  position: absolute;
  top: 0;
  left: 100%;
}

.box {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.box h1 {
  font-size: 50px;
  text-align: center;
}

.box1 {
  background-image: url("@/assets/section3.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.box2 {
  background: crimson;
  background-image: url("@/assets/section4.png");
  background-size: cover;
  background-repeat: no-repeat;
}

.box3 {
  background: darkorchid;
  background-image: url("@/assets/section5.png");
  background-size: cover;
  background-repeat: no-repeat;
}

#section6 {
  background: indianred;
  background-image: url("@/assets/section6.png");
  background-size: cover;
  background-repeat: no-repeat;
}

#section7 {
  background: paleturquoise;
  background-image: url("@/assets/section7.png");
  background-size: cover;
  background-repeat: no-repeat;
}
</style>
