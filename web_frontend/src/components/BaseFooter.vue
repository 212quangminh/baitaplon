<template>
   <footer id="footer">
      <div class="first-footer">
         <div class="container">
            <div class="d-flex justify-content-between">
               <div class="contact">
                  <h5>Thông tin liên hệ</h5>
                  <ul>
                     <li class="address">
                        <i class="fa-sharp fa-solid fa-location-dot icon-contact"></i>
                        Đại học Cần Thơ
                     </li>
                     <li class="phone">
                        <i class="fa-solid fa-phone icon-phone"></i>
                        <a style="color: orange;text-decoration: none;" href="tel:+84 56668888">+847963921246</a>
                     </li>
                     <li class="email">
                        <i class="fa-solid fa-envelope icon-email"></i>
                        <a style=" color: orange;ext-decoration: none;" href="mailto:kiettruong@gmail.com">quangminh2021202@gmail.com</a>

                     </li>
                  </ul>
               </div>
              
               <div class="column">
                  <h5>Mạng xã hội</h5>
                  <ul>
                     <li>
                        <i class="fa-brands fa-facebook"></i>
                        <a href="https://www.facebook.com"> Facebook</a>
                     </li>
                     <li>
                        <i class="fa-brands fa-twitter"></i>
                        <a href="https://www.twitter.com"> Twitter</a>
                     </li>
                     <li>
                        <i class="fa-brands fa-instagram"></i>
                        <a href="https://www.instagram.com"> Instagram</a>
                     </li>
                  </ul>
               </div>
             
            </div>
         </div>
      </div>
   </footer>
</template>

<script>
export default {};
</script>

<style scoped>
#footer {
   display: block;
}

.first-footer {
   background-color: #fff;
   color: orange;
   padding: 20px;
}

#footer h5 {
   font-size: 18px;
   color: orange;
   margin: 0 0 15px 0;
   padding: 0 0 7px 0;
   font-weight: normal;
}

#footer .contact ul {
   list-style: none;
   padding: 0;
}

#footer .contact ul li {
   color: orange;
   text-decoration: none;
   display: block;
   padding: 3px 0;
   line-height: 20px;
   font-size: 14px;
}

#footer .icon-contact {
   margin-right: 5px;
   font-size: 16px;
}

#footer .contact ul li+li {
   margin-top: 12px;
}

#footer .column ul {
   list-style: none;
   padding: 0;
}

#footer .column ul li a {
   color: orange;
   text-decoration: none;
   line-height: 18px;
   font-size: 15px;

}

#footer .column  ul li:hover {
   padding-left: 5px;
}

</style>
