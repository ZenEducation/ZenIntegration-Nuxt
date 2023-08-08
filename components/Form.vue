<template>
    <div class="container">
        <h1>Contact Form</h1>
        <form class="form" @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="name">Name:</label>
                <input type="text" id="name" name="name" v-model="formData.name" @input="handleChange" required />
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" id="email" name="email" v-model="formData.email" @input="handleChange" required />
            </div>
            <div class="form-group">
                <label for="message">Message:</label>
                <textarea id="message" name="message" v-model="formData.message" @input="handleChange" required></textarea>
            </div>
            <button type="submit">Submit</button>
            <br />
            <nuxt-link to="/form-details">
                <button type="button">Form Details</button>
            </nuxt-link>
        </form>
    </div>
</template>

<script>
import { ref } from 'vue';
import { DataStore } from "aws-amplify";
import {Todo} from "../src/models"
export default {
    setup() {
        const formData = ref({
            name: '',
            email: '',
            message: '',
        });

        const handleChange = (e) => {
            const { name, value } = e.target;
            formData[name] = value;
        };

        const handleSubmit = async(e) => {
            e.preventDefault();
             const res = await DataStore.save(
                new Todo(formData.value)
            );
            console.log('data', res);
            // Perform form submission logic here
            formData.name = '';
            formData.email = '';
            formData.message = '';
        };

        return {
            formData,
            handleChange,
            handleSubmit,
        };
    },
};
</script>






<style scoped>
.container {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    /* margin-top: 20px; */
}

a {
    display: flex;
    justify-content: center;
    text-decoration: none;
}


h1 {
    font-size: 24px;
    margin-bottom: 20px;
}

.form {
    display: flex;
    flex-direction: column;
    width: 380px;
}

.form-group {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
}

label {
    font-size: 16px;
    margin-bottom: 5px;
}

input,
textarea {
    padding: 8px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 10px 15px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
}

button:hover {
    background-color: #0056b3;
}
</style>