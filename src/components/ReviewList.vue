<script setup>
    defineProps({
        reviews:{
            type: Array,
            required: true
        }
    });
</script>

<template>
    <div class="review-container">
        <h3>Reseñas:</h3>
        <ul>
            <li 
                v-for="(review, index) in reviews" 
                :key="index"
            >
                    <span>{{ review.name }} dió {{ review.rating }} estrellas</span>
                    <br/>
                    <span>"{{review.content}}"</span>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    .review-list {
        border-top: 1px solid #eee;
        padding-top: 15px;
    }

    .review-item {

    }


    .review-container {
        background: #f8f7ff;
        border-radius: 10px;
        padding: 12px;
        margin: 20px 0 ;
    }


</style>