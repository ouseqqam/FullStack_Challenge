<template>
    <div>
        <h1>Add Category</h1>
        <div>
            <form @submit="addCategory">
                <input type="text" v-model="category.name" placeholder="Category Name">
                <input type="text" v-model="category.parent" placeholder="Add parent category if exist">
                <button type="submit">Add Category</button>
            </form>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue'
    import axios from 'axios'
    
    const category = ref({
        name: '',
        parent: ''
    })

    const addCategory = async (e) => {
        e.preventDefault()
        if (category.value.name === '') {
            alert('Please enter category name')
            return
        }
        
        try {
            if (category.value.parent === '') {
                delete category.value.parent
            }
            const res = await axios.post('http://localhost:4200/api/category/store', category.value)
            console.log(res.data)
        } catch (err) {
            console.log(err)
        }
    }
</script>
