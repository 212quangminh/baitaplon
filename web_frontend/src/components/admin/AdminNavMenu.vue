<template>
   <nav class="navbar navbar-expand-lg navbar-light">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
         aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
         <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
         <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
               <router-link to="/" class="nav-link">
                  <i class="fa-solid fa-house"></i>
               </router-link>
            </li>
            <li class="nav-item">
               <router-link to="/adminpage" class="nav-link">Quản lý sản phẩm</router-link>
            </li>
            <li class="nav-item">
               <router-link to="/user" class="nav-link">Quản lý tài khoản</router-link>
            </li>
         </ul>
         <ul class="navbar-nav">
            <li class="nav-item" v-if="this.local_user.role != ''">
               <router-link to="/login" class="nav-link" @click="handleLogout">
                  <b>{{ this.local_user.name }}</b>
                  <button class="btn logout-btn">
                     <i class="fa-solid fa-user"></i>
                  </button>
               </router-link>
            </li>
         </ul>

      </div>
   </nav>
</template>

<script>
import ProductList from "../../views/products/ProductList.vue";

export default {
   components: {
      ProductList,
   },
   data() {
      return {
         local_user: {},
      };
   },
   methods: {
      handleLogout() {
         localStorage.removeItem("localUserLogin");
      },
   },
   mounted() {
      const user = JSON.parse(localStorage.getItem("localUserLogin"));
      this.local_user = user;
   },
};
</script>

<style scoped>
.navbar {
   border-top: 1px solid #E38B29;
   border-bottom: 1px solid #E38B29;
   border-right: 0;
   border-left: 0;
}

.navbar .nav-item {
   color: #E38B29;
   position: relative;
}

.navbar .nav-item a {
   font-family: "Open Sans", sans-serif;
   color: #E38B29 !important;
   text-align: left;
   font-size: 16px;
}

.navbar .nav-item a:hover {
   color: #E38B29 !important;
   border-radius: 10px;
   box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.nav-item ul li a {
   display: flex;
   text-align: left;
}

.user_name {
   margin-left: 620px;
   text-transform: uppercase;
}

i {
   color: #E38B29;
}

.logout-btn {
   width: 30px;
   height: auto;
   padding: 0px !important;
   margin-top: -5px;
   margin-left: 5px;
}
</style>
