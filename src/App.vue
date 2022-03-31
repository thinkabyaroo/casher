<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-lg-8">
      </div>
      <div class="col-lg-4">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title mb-3">ကုန်ပစ္စည်း</h3>
            <form action="" @submit.prevent="saveRecord">
              <div class="my-3">
                <select class="form-select mb-3" v-model="selectedProduct" id="">
                  <option value="">Selected Product</option>
                  <option v-for="product in products" :value="product.id" :key="product.id">
                    {{product.name}}
                  </option>
                </select>
<!--                <div>-->
<!--                  <select class="form-select" v-model="selectedUnit">-->
<!--                    <option v-if="selectedProduct === 0">Select Unit</option>-->
<!--                    <option v-else="selectedProduct >0" v-for="unit in selectedProductDetail.unit" :key="unit.id" >-->
<!--                      {{unit.name}}-->
<!--                    </option>-->

<!--                  </select>-->
<!--                </div>-->
                <div v-if="selectedProduct >0">
                  <select class="form-select mb-3" v-model="selectedUnit" id="">
                    <option value="">Select Unit</option>
                    <option v-for="unit in selectedProduct>0 && selectedProductDetail.unit" :value="unit.id">
                      {{unit.name}} - [{{unit.price}}ကျပ် ]
                    </option>
                  </select>
                </div>
<!--                <div v-else>-->
<!--                  <select class="form-select mb-3" id="">-->
<!--                    <option value="">Select Unit</option>-->
<!--                  </select>-->
<!--                </div>-->

                <div class="mb-3">
                  <input type="number" placeholder="quantity" class="form-control" v-model="inputQuantity">
                </div>
              </div>
              <div class="" @click="saveRecord">
                <button class="btn btn-primary">Add</button>
              </div>

            </form>
<!--            {{records}}-->

            <table class="table table-bordered mt-3">
              <thead>
              <tr>
                <th>#</th>
                <th>ပစ္စည်း</th>
                <th>Unit / Price</th>
                <th>Quantity</th>
                <th>Cost</th>
              </tr>
              </thead>
              <tbody>
              <tr>
                <td v-if="records.length === 0" colspan="5" class="text-center">No record</td>
              </tr>
              <tr class="animate__animated animate__fadeInDown" v-for="record in records" :key="record.id">
                <td>
                  <span class="show-in-print">{{ record.id }}</span>
                  <i @click="del(record.id)" class="fa-solid fa-trash-alt text-danger hide-in-print"></i>
                </td>
                <td>{{ record.product.name }}</td>
                <td class="text-end">{{ record.unit.price }} ကျပ်  /{{record.unit.name}}</td>
                <td class="text-end">{{ record.quantity }}</td>
                <td class="text-end">{{ record.cost }}</td>
              </tr>
              </tbody>
              <tfoot>
              <tr v-if="records.length > 0">
                <td colspan="4">Total</td>
                <td class="text-end">{{ records.reduce((pv,cv)=>pv+cv.cost,0) }}</td>
              </tr>
              </tfoot>
            </table>



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
      inputQuantity:null,
      recordStart:1,
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
          id:3,
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
          id:4,
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
      ],
      records:[],
    }
  },
  computed: {
    selectedProductDetail() {
      if (this.selectedProduct === null){
        return {}
      }
      return this.products.find(el=>el.id === this.selectedProduct)
    }
  },
  methods: {

    saveRecord() {
      let currentUnit=this.selectedProductDetail.unit.find(el=>el.id === this.selectedUnit)
      let record={
        id:this.recordStart,
        product:this.selectedProductDetail,
        unit:currentUnit,
        quantity:this.inputQuantity,
        cost:currentUnit.price * this.inputQuantity
      };
      //this.records.push(record);
      this.records=[...this.records,record]
      console.log(record);
      
      this.selectedProduct=this.selectedUnit=this.inputQuantity=""
      this.recordStart++

      // console.log(this.selectedProductDetail,this.selectedProduct,this.selectedUnit,this.inputQuatity)
    }
  },
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free/css/all.min.css";
</style>