<template>
    <div>
        <h1 class="title has-text-centered mt-5">Edit Product</h1>
        <div class="field">
            <label class="label">Product Name</label>
            <div class="control">
                <input class="input" type="text" placeholder="Product Name" v-model="productName"/>
            </div>
        </div>
        <div class="field">
            <label class="label">Product Price</label>
            <div class="control">
                <input class="input" type="text" placeholder="Price" v-model="productPrice"/>
            </div>
        </div>
        <div class="control">
            <button class="button is-warning" @click="updateProduct">UPDATE</button>
        </div>
    </div>
</template>

<script>
    // import axios
    import axios from "axios";
    export default {
        name: "ProductEdit",
        data() {
            return {
                productName: "",
                productPrice: "",
            };
        },
        created: function () {
            this.getProductById();
        },
        methods: {
            // Get Product By Id
            async getProductById() {
                try {
                    const response = await axios.get(
                        `http://localhost:3000/api/products/${this.$route.params.id}`
                    );
                    this.productName = response.data.response[0].product_name;
                    this.productPrice = response.data.response[0].product_price;
                } catch (err) {
                    console.log(err);
                }
            },
            // Update product
            async updateProduct() {
                try {
                    await axios.put(
                        `http://localhost:3000/api/products/${this.$route.params.id}`,
                        {
                            product_name: this.productName.trim(),
                            product_price: this.productPrice,
                        }
                    );
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