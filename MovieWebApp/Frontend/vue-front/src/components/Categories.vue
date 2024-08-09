<template>
  <div>
    <h1>Movie Categories</h1>
    <ul>
      <li class="genres" v-for="category in categories" :key="category.id">
        {{ category.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const categories = ref([]);

    const fetchCategories = async () => {
      try {
        const response = await axios.get(
          "https://localhost:7282/api/Categories"
        );
        categories.value = response.data.genres;
        console.log(categories.value);
      } catch (error) {
        console.error("Error fetching movie categories:", error);
      }
    };

    onMounted(() => {
      fetchCategories();
    });

    return {
      categories,
    };
  },
};
</script>

<style scoped>
.genres {
  @apply bg-blue-400 rounded-xl my-3 flex flex-col justify-center;
}
</style>
