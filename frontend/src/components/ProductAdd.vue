<template>
    <div>
        <h1 class="title has-text-centered mt-5">Add Product</h1>
        <div class="field">
            <label class="label">Product Name</label>
            <div class="control">
                <input class="input" type="text" placeholder="Product Name" v-model="productName" autofocus/>
            </div>
        </div>
        <div class="field">
            <label class="label">Product Price</label>
            <div class="control">
                <input class="input" type="text" placeholder="Product Price" v-model="productPrice"/>
            </div>
        </div>
        <div class="control">
            <button class="button is-success" @click="saveProduct">SAVE</button>
        </div>
    </div>
</template>

<script>
    // import axios
    import axios from "axios";
    export default {
        name: "ProductAdd",
        data() {
            return {
                productName : "",
                productPrice: "",
            };
        },
        methods: {
            // Create New product
            async saveProduct() {
                try {
                    await axios.post("http://localhost:3000/api/products", {
                        product_name: this.productName.trim(),
                        product_price: this.productPrice,
                    });
                    this.productName = "";
                    this.productPrice = "";
                    this.$router.push("/");
                } catch (err) {
                    console.log(err);
                }
            },
        },
    };
</script>

<style>
</style>