<template>
  <div>
    <div class="container">
      <h1 class="text-center">Workshop Vue#1 Input Max value</h1>
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span v-text="max - massage.length" class="input-group-text"></span>
        </div>
        <input
          v-model="massage"
          :maxlength="max"
          type="text"
          class="form-control"
        />
      </div>
      <hr class="my-4" />
      <h1 class="text-center">Workshop Vue#2 Preview Img</h1>
      <div>
        <div v-if="!img" class="input-group mb-3">
          <input type="file" class="form-control" @change="onFileChange" />
        </div>
        <div v-else>
          <img :src="img" class="img-fluid" />
          <button class="btn btn-danger" @click="remove">Remove</button>
        </div>
      </div>
      <hr class="my-4" />
      <h1 class="text-center">Workshop Vue#3 Total Price Product</h1>
      <div class="row">
        <div v-for="item in products" :key="item.id" class="col-md-4">
          <div class="card h-100">
            <img :src="item.image" class="card-img-top" alt="" />
            <div class="card-body">
              <h4 class="card-title">{{ item.name }}</h4>
              <h3 class="card-text">ราคา {{ item.price }} บาท</h3>
            </div>
            <div class="card-footer text-center">
              <input
                type="checkbox"
                class="btn-check"
                :id="item.id"
                autocomplete="off"
                @change="select(item)"
              />
              <label class="btn btn-outline-primary" :for="item.id"
                >เลือก</label
              >
            </div>
          </div>
        </div>
        <h2>Total : {{total()}} Bath</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      massage: "",
      max: 20,

      img: "",

      products: [
        {
          id: 1,
          name: "Coffee",
          price: 80,
          image:
            "https://upload.wikimedia.org/wikipedia/commons/4/45/A_small_cup_of_coffee.JPG",
          active: false,
        },
        {
          id: 2,
          name: "Tea",
          price: 100,
          image:
            "https://upload.wikimedia.org/wikipedia/commons/0/04/Masala_Chai.JPG",
          active: false,
        },
      ],
    };
  },
  methods: {
    remove() {
      this.img = "";
    },
    onFileChange(e) {
      const files = e.target.files[0];
      const reader = new FileReader();
      reader.onload = (e) => {
        this.img = e.target.result;
      };
      reader.readAsDataURL(files);
    },
    select(item) {
      item.active = !item.active;
    },
    total() {
      let sum = 0;
      this.products.forEach((item) => {
        if (item.active) {
          sum += item.price;
        }
      });
      return sum;
    },
  },
};
</script>

<style></style>
