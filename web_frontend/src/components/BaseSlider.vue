<template>
   <div class="slider-box">
      <div class="slider-content">
         <Splide :options="options" aria-label="My Favorite Images">
            <SplideSlide>
               <img src="https://media-cdn-v2.laodong.vn/Storage/NewsPortal/2023/1/27/1141740/Kobe-Bryant.jpg" alt="Sample 2" />
            </SplideSlide>
            <SplideSlide>
               <img src="https://tophinhanhdep.com/wp-content/uploads/2021/10/4K-NBA-Wallpapers-1024x576.jpg" alt="Sample 1" />
            </SplideSlide>
            <SplideSlide>
               <img src=" https://s.yimg.com/ny/api/res/1.2/kV.EsRb1DTO3f6kbFLQHHQ--/YXBwaWQ9aGlnaGxhbmRlcjt3PTY0MDtoPTQyNw--/https://s.yimg.com/os/creatr-uploaded-images/2022-07/06c0c250-0154-11ed-bfee-ec86f69b309e" alt="">
            </SplideSlide>
            <SplideSlide>  
               <img src="https://w0.peakpx.com/wallpaper/654/248/HD-wallpaper-basketball-ja-morant.jpg" alt="">
            </SplideSlide>
         </Splide>
      </div>
   </div>
</template>

<script>
import { Splide, SplideSlide } from "@splidejs/vue-splide";
import { defineComponent } from "vue";

export default defineComponent({
   components: {
      Splide,
      SplideSlide,
   },

   setup() {
      const options = {
         rewind: true,
         gap: "1rem",
         autoplay: true,
      };

      return { options };
   },
});
</script>

<style scoped>
.splide__slide img {
   width: 100%;
   height: 500px;
   object-fit: cover; /* Bao phủ toàn bộ khung hình */
   display: block;
}
.content {
   margin-top: 5px;
   position: absolute; /* Để đưa nội dung vào trong khung ảnh */
   right: 10px;
   bottom: 20px;
   width: 400px;
   text-align: justify;
   background-color: #333;
   padding: 7px 7px 12px;
   border-radius: 3px;
   opacity: 0.85;
}
.content a {
   text-decoration: none;
   color: white;
   display: inline-block;
   line-height: 24px;
   text-transform: uppercase;
}
</style>
