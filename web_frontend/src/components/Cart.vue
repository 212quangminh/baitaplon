<template>
   <div class="wrapper">
      <div class="header">
         <div class="nav-menu">
            <NavMenu />
         </div>
      </div>
      <div class="container">
         <div class="px-3 py-3 pr-3 mx-auto float-left">
            <span class="btn btn-success">
               Số sản phẩm: {{ products.length }}
            </span>
         </div>
         <div class="px-3 py-3 pr-3 mx-auto float-right">
            <button class="btn btn-success">
               Tổng:
               {{
                  `${totalPrice().replace(/\B(?=(\d{3})+(?!\d))/g, ".")} đồng`
               }}
            </button>
         </div>
         <table class="table table-bordered table-striped table-sm">
            <thead>
               <tr class="table-active text-center">
                  <th scope="col">STT</th>
                  <th scope="col">Hình ảnh</th>
                  <th scope="col" class="space-name">Tên sản phẩm</th>
                  <th scope="col" class="space-price">Giá</th>
                  <th scope="col" class="space-amount">Số lượng</th>
                  <th scope="col" class="space-total">Thành tiền</th>
                  <th scope="col" class="space-handle">Xử lý</th>
               </tr>
            </thead>
            <tbody>
               <tr :key="index" v-for="(product, index) in products">
                  <td class="items-center text-center">{{ index + 1 }}</td>
                  <td>
                     <img class="product-img" :src="product.imgUrl" alt="" />
                  </td>
                  <td class="items-center">
                     {{ product.name }} {{ product.description }}
                  </td>
                  <td class="items-center text-center">
                     {{ product.price.replace(/\B(?=(\d{3})+(?!\d))/g, ".") }}
                     đồng
                  </td>
                  <td class="items-center text-center"><input class="amount" min="0" type="number" v-model="product.amount"/></td>
                  <td class="items-center text-center">
                     {{
                        `${product.price * product.amount}`.replace(
                           /\B(?=(\d{3})+(?!\d))/g,
                           "."
                        )
                     }}
                     đồng
                  </td>
                  <td class="items-center text-center">
                     <button
                        v-if="product.id"
                        type="button"
                        class="ml-2 btn btn-danger"
                        @click="deleteProductCart(index)"
                     >
                        Xóa
                     </button>
                  </td>
               </tr>
            </tbody>
         </table>
      </div>
   </div>
</template>

<script>
import NavMenu from "../components/NavMenu.vue";

export default {
   components: {
      NavMenu,
   },
   data() {
      return {
         products: [],
      };
   },
   methods: {
      deleteProductCart(index) {
         const filteredProductCart = this.products.filter(
            (product) => product.id != this.products[index].id
         );
         this.products = filteredProductCart;
         const localProductCart = JSON.stringify(filteredProductCart);
         localStorage.setItem("localProductCart", localProductCart);
      },
      totalPrice() {
         let total = 0;
         for (let i = 0; i < this.products.length; i++) {
            total += this.products[i].price * this.products[i].amount;
         }
         return `${total}`;
      },
   },
   mounted() {
      const listLocalCart = JSON.parse(
         localStorage.getItem("localProductCart") ?? "[]"
      );
      this.products = listLocalCart;
   },
};
</script>
<style scoped>
.wrapper {
   max-width: 100%;
   background: #fff;
   font-family: "Open Sans", sans-serif;
   padding-bottom: 50px;
}
.header {
   width: 100%;
   /* height: 210px; */
   height: auto;
}
.container {
   background-color: #fff;
   margin-top: 10px;
}
.amount{
   width: 50px;
}
.product-list {
   padding-bottom: 10px;
}
.product-img {
   width: 150px;
   height: auto;
}
a {
   text-decoration: none;
}
.button-add {
   color: #fff;
}
.space-price {
   width: 150px;
}
.space-amount {
   width: 100px;
}
.space-total {
   width: 150px;
}
.space-handle {
   width: 150px;
}
.items-center {
   padding-top: 45px;
}
</style>
