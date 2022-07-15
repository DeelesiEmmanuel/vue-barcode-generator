<template>
  <form @submit.prevent="downloadBarCode()" class="form">
  <h1>Type to view BarCode</h1>
    <div ref="barCodeDiv">
      <vue-barcode
        ref="BarImg"
        v-if="BarcodeValue"
        tag="img"
        :value="BarcodeValue"
        :options="{ displayValue: true, lineColor: '#2B2B2C' }"
      />
    </div>
    <input type="text" v-model="BarcodeValue" />
    <button v-if="BarcodeValue">Save BarCode</button>
    
  </form> 
</template>

  <script>
import VueBarcode from "@chenfengyuan/vue-barcode";
import html2canvas from "html2canvas"; // imported the html2canvas package

export default {
  data() {
    return {
      BarcodeValue: null,
    };
  },
  components: {
    "vue-barcode": VueBarcode,
  },
  methods: {
    downloadBarCode() {
      html2canvas(this.$refs.barCodeDiv).then((canvas) => {
        var barcodeImgTag = document.createElement("a");
        document.body.appendChild(barcodeImgTag);
        barcodeImgTag.download = "Barcode.jpg";
        barcodeImgTag.href = canvas.toDataURL();
        barcodeImgTag.target = "_blank";
        barcodeImgTag.click();
      });
    },
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.form {
display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
button {
  height: 40px;
  width: 310px;
  background-color: green;
  color: white;
  border: none;
  border-radius: 0.5rem;
  font-size: medium;
  display: block;
  margin-top: 1.3rem;
}
input {
  height: 30px;
  width: 300px;
  padding: 5px;
  font-size: 1rem;
  border-radius: 7px;
}
</style>
