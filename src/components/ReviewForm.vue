<script setup>
    import {reactive} from 'vue';
// Funciones guardar reseñas
    const emit= defineEmits(['review-submitted']);
    const review = reactive({
        name: '',
        content: '',
        rating: null,
    });

    function onSubmit() {
        if (review.name === '' || review.content === '' || review.rating === null) {
            alert('La reseña está incompleta. Por favor, llena todos los campos.')
            return
        }
        const productReview = {
            name: review.name,
            content: review.content,
            rating: review.rating,
        }
        emit('review-submitted', productReview);

        // limpiar el formulario
        review.name = ''
        review.content = ''
        review.rating = null
    };
</script>
<template>
    <form  
        class="review-form" 
        @submit.prevent="onSubmit"
        >
            <h3>Deja un comentario</h3>
            <label for="name">Nombre:</label>
            <input 
                id="name"
                v-model="review.name">

            <label for="review">Comentario:</label>
            <textarea  
                id="review" 
                v-model="review.content"
            >
            </textarea>

            <label for="rating">Calificacion:</label>
            <select 
                id="rating" 
                v-model.number="review.rating"
            >
                    <option>5</option>
                    <option>4</option>
                    <option>3</option>
                    <option>2</option>
                    <option>1</option>
            </select>

            <input 
                type="submit" 
                class="btn-submit" 
                value="submit"
            >
    </form>
</template>
<style scoped>
    .review-form {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-bottom: 25px;
    }

    label {
        font-weight: bold;
        color: #403f43ff;
    }

    input,
    textarea,
    select {
        border: 1px solid #c9c9c9;
        border-radius: 8px;
        padding: 8px 10px;
        font-size: 15px;
        outline: none;
        transition: border-color 0.3s ease;
    }

    input:focus,
    textarea:focus,
    select:focus {
        border-color: #984fcf8a;
    }

    textarea {
        resize: none;
        min-height: 70px;
    }

    .btn-submit {
        background-color: #8882b8ff;
        color: white;
        border: none;
        border-radius: 8px;
        padding: 10px;
        font-size: 16px;
        margin: 10px 0 10px;
        cursor: pointer;
        width:20%;
        align-self: start;
    }

    .btn-submit:hover {
        background-color: #4a3aff;
    }
</style>