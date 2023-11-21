<template>
      <div class="container">
         <div class="row">
            <div id="content" class="col-sm-12 page">
               <div class="header-content ">
                  <!-- d-flex flex-row-reverse -->
                  <form class="form-inline my-2 my-lg-0 p-2">
                     <input class="form-control mr-sm-2 " type="search" placeholder="Search" aria-label="Search"
                        v-model="searchText">
                     <button class="btn btn-outline-success my-2 my-sm-0" type="submit"><i class="fas fa-search" data-v-f13c8677=""></i></button>
                  </form>
               </div>
               <div class="row product-category">
                  <div v-if="filteredProductsCount > 0"></div>
                  <p class="non-product" v-else>Không có sản phẩm nào</p>
                  <div class="product-grid col-lg-3" :key="index" v-for="(product, index) in filteredProducts">
                     <div class="thumb">
                        <div class="image">
                           <a href="#"><img :src="product.imgUrl" alt="Sản phẩm" /></a>
                        </div>
                        <div class="caption">
                           <h4>
                              <a href="#" class="product-name">
                                 <b>{{ product.name }}</b>
                                 <br>
                                 {{ product.description }}
                              </a>
                           </h4>
                           <p class="price">
                              {{
                                 product.price.replace(/\B(?=(\d{3})+(?!\d))/g, ".")
                              }}
                              đồng
                           </p>
                        </div>
                        <div class="botton-cart">
                           <button class="btn-cart" @click="addProductToCart(index)">
                              Thêm vào giỏ
                           </button>
                        </div>
                     </div>
                  </div>
               </div>
            </div>
         </div>
      </div>
</template>

<script>
import ProductService from "../services/product.service";

export default {
   data() {
      return {
         products: [],
         searchText: "",
      };
   },

   computed: {
      productStrings() {
         return this.products.map((product) => {
            const { name, description } = product;
            return [name, description].join("");
         });
      },
      filteredProducts() {
         if (!this.searchText) return this.products;
         return this.products.filter((_product, index) =>
            this.productStrings[index].includes(this.searchText)
         );
      },
      filteredProductsCount() {
         return this.filteredProducts.length;
      },
   },
   methods: {
      async getAllProduct() {
         try {
            this.products = await ProductService.getAll();
         } catch (error) {
            console.log(error);
         }
      },
      async addProductToCart(index) {
         const saveLocalCart = JSON.parse(
            localStorage.getItem("localProductCart") ?? "[]"
         );
         for (const item of saveLocalCart) {
            if (item.id === this.products[index]._id) {
               item.amount++;
               const localProductCart = JSON.stringify(saveLocalCart);
               localStorage.setItem("localProductCart", localProductCart);
               alert(
                  `Số lượng sản phẩm ${this.products[index].name} đã được cập nhật`
               );
               return;
            }
         }
         const temp = {
            id: this.products[index]._id,
            name: this.products[index].name,
            imgUrl: this.products[index].imgUrl,
            price: this.products[index].price,
            description: this.products[index].description,
            amount: 1,
         };
         saveLocalCart.push(temp);
         const localProductCart = JSON.stringify(saveLocalCart);
         localStorage.setItem("localProductCart", localProductCart);
         alert(
            `Sản phẩm ${this.products[index].name} vừa được thêm vào giỏ hàng`
         );
      },
   },

   created() {
      this.getAllProduct();
   },
};
</script>

<style scoped>


.row {
   padding-top: 0px;
   /* padding: 0px; */
}
.btn-outline-success{
   background-color: #fff;
}
#content {
   min-height: 400px;
}

.product-category {
   padding-top: 25px;
   padding-bottom: 29px;
   display:flex;
   /* justify-content: space-around; */
   border:1px solid #fff;
   background-color: #fff;
}
 .fa-search{
   color:black;
}
.header-content {
   /* display: flex; */
   padding: 10px 0px 10px 0px;
   /* border-bottom: 3px solid #E38B29; */
   font-weight: normal;
   font-size: 22px;
}
input{
   flex:1;
}
.page{
   padding: 0px;
}

.non-product {
   margin-left: 450px;
   margin-top: 15px;
   font-size: 20px;
   font-weight: bold;
   color:#E38B29;
}

.product-grid {
   height: 300px;
   
   /* position: relative; */
   text-align: center;
   vertical-align: top;
   padding: 7px;
   margin:20px 0px 0px 0px;
   /* border: 1px solid black;*/
   background-color:transparent;
}
.caption{
   color:#E38B29;
}
.product-grid .thumb img {
   /* object-fit: cover; */
   height: 150px;
}

.product-grid .thumb .caption h4 a {
   font-size: 13px;
   line-height: 22px;
   text-decoration: none;
   padding: 5px;
   color:#E38B29;
   margin: 0 auto;
   width: 100%;
   overflow: hidden;
   text-overflow: ellipsis;
   -webkit-line-clamp: 2;
   display: -webkit-box;
   -webkit-box-orient: vertical;
}

.product-grid:hover {
   transform: scale(1.2);
}

.price {
   color: #ff0000;
   font-weight: bold;
}



.botton-cart {
   position: absolute;
   bottom: 0;
   left: calc(50% - 55px);
}

.btn-cart {
   background-color: #E38B29;
   color:  #fff;
   border: 1px;
   border-radius: 3px;
}

.btn-cart:hover {
   background-color: #fff;
}</style>
