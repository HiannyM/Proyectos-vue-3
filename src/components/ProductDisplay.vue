<script setup>
    import ReviewForm from '../components/ReviewForm.vue';
    import ReviewList from '../components/ReviewList.vue';

    import {ref, computed} from 'vue';
    
    const product = ref("Cat socks");
    const brand= ref('Fashion brand Company ');
    const title = computed (()=>{
        return brand.value+''+product.value
    });
//Agregar un imagen a una etiqueta
    import CatSocks  from "../assets/images/CatSocks.jpg";
    import GatitoTuxedo from "../assets/images/GatitoTuxedo.jpg";
    import GatitoAngora from "../assets/images/GatitoAngora.jpg";

    const image = ref(CatSocks);

//Mostrar disponibilidad del producto
    const inventory = ref(20);
// Mostrar en array las variantes del producto
    const variants = ref([
        {id: 2234, color: 'Gray', image: CatSocks},
        {id: 3320, color: 'Black', image: GatitoTuxedo},
        {id: 3234, color: 'Pink', image: GatitoAngora}
    ]);

    const sizes = ref(["S","M","L","XL"]);

//Funciones btn agregar producto al carrito
    const cart= ref(0);
    const addToCart = ()=>{

        cart.value += 1;
    };
    const quitToCart= ()=>{
        cart.value -= 1;
        if (cart.value<=-1) {
            cart.value = 0;
        }
    };

    const updateImage =(variantImage)=>{
        image.value = variantImage;
    };
// Para hacer submit en el form de resenas
    const reviews = ref([]);
    const addReview = (review)=>{
        reviews.value.push(review);
    };

</script>

<template>
    <div class="cart">
        <p>Carrito ({{ cart}})</p>
    </div>

    <div class="product-card">
            <div class="product-img">
                <img 
                    :src="image" 
                    alt="Producto" 
                />
            </div>

        <div class="product-info">
            <h1 class="product-name">           
                {{ title }}
            </h1>

            <p 
                v-if="inventory > 10" 
                class="stock-product"
                style="color: #199f04ff;"
            >
                Disponible.
            </p>

            <p 
                v-else-if="inventory > 0" 
                class="stock-product "
                style="color: #bfbf0eff;"
            >
                ¡Casi agotado!
            </p>

            <p 
                v-else class="stock-product"
                style="color: #a63230ff;"

            >
                ¡Agotado!
            </p>


            <ul class="size-product">
                <h3>Sizes:</h3>
                <li 
                    v-for="size in sizes" 
                    :key="size"
                >
                    <a href="#">{{ size }}</a>
                </li>
            </ul>

            <div class="variants">
                <button
                    v-for="variant in variants"
                    :key="variant.id"
                    class="circleColor"
                    :style="{ backgroundColor: variant.color }"
                    @mouseover="updateImage(variant.image)"
                >
                </button>
            </div>

            <div class="btn-cart">
                <button
                    class="addCart"
                    :disabled="!inventory"
                    :class="{ 'disabled-button': !inventory }"
                    @click="addToCart"
                >
                    Añadir al carrito
                </button>
                <button 
                    class="quitCart" 
                    @click="quitToCart"
                >
                    Quitar del carrito
                </button>
            </div>
        </div>
    </div>

    <ReviewList 
        v-if="reviews.length > 0" 
        :reviews="reviews"></ReviewList>
    <ReviewForm 
        @review-submitted="addReview"
    >
    </ReviewForm>
</template>

<style scoped>
    h1{
            font-size:20px;
            

    }
    .product-name {
    margin: 0;
    padding-top:20px;
    color: #151516ff;
    font-size: 20px;
    font-weight: 700;
    }

    .product-card {
        display: flex;
        gap: 24px;
        background: linear-gradient(180deg, #ffffff 0%, #faf8ff 100%);
        border-radius: 14px;
        padding: 20px;
        box-shadow: 0 12px 30px rgba(37, 27, 104, 0.08);
        align-items: flex-start;
    }

    .product-img  {
    background: #fff;
    border-radius: 12px;
    padding: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: inset 0 2px 6px rgba(0,0,0,0.03);
}

    .product-img img{
        width: 100%;
        max-width: 420px;
        height: auto;
        border-radius: 10px;
        object-fit: cover;
    }
    .product-card {
        margin-top: 12px;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .product-info {
        font-size: 14px;
        color: #000f;
        font-weight: 600;    
    }

    .circleColor {
    border-radius: 50%;
    border: 1px solid #444;
    height: 20px;
    width: 20px;
    margin: 5px;
    cursor: pointer;
    }

    .disabled-button {
    background-color: #ccc;
    cursor: not-allowed;
    }
    .cart  {
        font-size: 20px;

    }

    .btn-cart button{
        padding:10px 14px;
        border-radius:10px;
        font-weight:700;   
        font-size:15px; 
    }
</style>
