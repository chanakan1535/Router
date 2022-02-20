<template>
  <div
    class="bg-image d-flex justify-content-center align-items-center"
    style="background-color: rgb(4, 40, 75)"
  >
    <v-container>
      <center><h1 style="color: white">Product</h1></center>
      <v-container class="d-flex flex-wrap">
        <v-card
          class="mx-auto mb-5"
          max-width="400"
          v-for="(i, index) in productlist"
          :key="index"
        >
          <v-img class="text-black align-end" height="350px" :src="i.imageurl">
            <v-card-title>{{ i.name }}</v-card-title>
          </v-img>

          <v-card-subtitle class="pb-0">{{ i.rightText }}</v-card-subtitle>

          <v-card-text class="text--primary">
            <div style="font-size: large">{{ i.leftText }}</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="info" text :to="'/detail/' + i.rightText"
              >detail</v-btn
            >
            <v-btn color="orange" @click="selected(i)"> Add </v-btn>
          </v-card-actions>
        </v-card>
      </v-container>

      <table class="table table-striped table-hover"></table>
      <v-container
        ><h4 class="text-danger fs-1">Total {{ total() }} Baht</h4></v-container
      >
      <v-container grid-list-xs class="white">
        <router-view :key="$route.path"></router-view>
      </v-container>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      productlist: [
        {
          name: "Sofa",
          imageurl:
            "data:image/jpeg;base64,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",
          rightText: "",
          leftText: "Price : 8,504",
          active: false,
          price: 8504,
        },

        {
          name: "Table home",
          imageurl:
            "https://www.ikea.com/th/th/images/products/ingo-table-pine__0737092_pe740877_s5.jpg?f=s",
          rightText: "",
          leftText: "Price : 15,900",
          active: false,
          price: 15900,
        },

        {
          name: "Computer",
          imageurl:
            "https://shopee.co.th/blog/wp-content/uploads/2021/05/%E0%B8%84%E0%B8%AD%E0%B8%A1%E0%B9%84%E0%B8%A1%E0%B9%88%E0%B9%80%E0%B8%81%E0%B8%B4%E0%B8%99-15000.jpg",
          rightText: "",
          leftText: "Price : 50,994",
          active: false,
          price: 50994,
        },
      ],
    };
  },
  methods: {
    selected: function (i) {
      i.active = !i.active;
    },
    total: function () {
      var sum = 0;
      this.productlist.forEach(function (i) {
        if (i.active) {
          sum += i.price;
        }
      });
      return sum;
    },
  },
};
</script>

<style>
h2 {
  color: white;
}
</style>
