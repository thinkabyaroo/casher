<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-lg-8">
      </div>
      <div class="col-lg-4">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title mb-3">Stocks</h3>
            <form action="">
              <div class="my-3">
                <select class="form-select" v-model="selectedProduct" id="">
                  <option value="">Selected Product</option>
                  <option v-for="product in products" :value="product.id" :key="product.id">{{product.name}}</option>
                </select>
                <div>
                  <select class="form-select" v-model="selectedUnit">
                    <option v-if="selectedProduct === 0">Select Unit</option>
                    <option v-else="selectedProduct >0" v-for="unit in selectedProductDetail.unit" :key="unit.id" >
                      {{unit.name}}
                    </option>

                  </select>
                </div>
              </div>

            </form>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedProduct:"",
      selectedUnit:"",
      products: [
        {
          id:1,
          name:"apple",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:110
            },
            {
              id:2,
              name:"ထုပ်",
              price:1000
            },
          ]
        },
        {
          id:2,
          name:"egg",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:150
            },
            {
              id:2,
              name:"ကဒ်",
              price:1200
            },
          ]
        },
        {
          id:1,
          name:"orange",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:100
            },
            {
              id:2,
              name:"ထုပ်",
              price:900
            },
          ]
        },
        {
          id:1,
          name:"banana",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:50
            },
            {
              id:2,
              name:"ဖီး",
              price:500
            },
          ]
        },
        {
          id:5,
          name:"ခေါက်ဆွဲ",
          unit:[
              {
                id:1,
                name:"ထုပ်",
                price:500
            },
            {
              id:2,
              name:"ဒါဇင်",
              price:4000
            }
          ]
        },
      ]
    }
  },
  computed: {
    selectedProductDetail() {
      if (this.selectedProduct === ""){
        return {}
      }
      return this.products.find(el=>el.id === this.selectedProduct)
    }
  },
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free/css/all.min.css";
</style>