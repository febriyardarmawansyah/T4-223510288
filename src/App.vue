<template>
  <div class="container">
    <form @submit.prevent="save" class="form">
      <input type="text" v-model="form.title" placeholder="Title" class="input" /><br />
      <textarea v-model="form.content" placeholder="Content" class="textarea"></textarea><br />
      <button type="submit" class="button">Save</button>
    </form>
    <ul class="articles-list">
      <li v-for="article in articles" :key="article.id" class="article">
        <div class="article-content">
          <h3>{{ article.title }}</h3>
          <p>{{ article.content }}</p>
        </div>
        <div class="article-actions">
          <button @click="edit(article)" class="button edit">Edit</button>
          <button @click="remove(article.id)" class="button delete">Delete</button>
        </div>
      </li>
    </ul>
    <button @click="load" class="button load">Load</button>
  </div>
</template>

<script>
import { ref, onMounted, reactive } from "vue";
import axios from "axios";

export default {
  setup() {
    const form = reactive({
      id: null,
      title: "",
      content: "",
    });

    const articles = ref([]);

    async function load() {
      try {
        const response = await axios.get("http://localhost:3000/articles");
        console.log("Articles loaded:", response.data); // Debugging log
        articles.value = response.data;
      } catch (error) {
        console.error("Error loading articles:", error);
      }
    }

    async function save() {
      try {
        const url = form.id
          ? `http://localhost:3000/articles/${form.id}`
          : "http://localhost:3000/articles";
        const method = form.id ? "put" : "post";
        const response = await axios[method](url, {
          title: form.title,
          content: form.content,
        });
        console.log("Article saved:", response.data); // Debugging log

        if (form.id) {
          articles.value = articles.value.map((article) =>
            article.id === form.id ? response.data : article
          );
        } else {
          articles.value.push(response.data);
        }

        form.id = null;
        form.title = "";
        form.content = "";
      } catch (error) {
        console.error("Error saving article:", error);
      }
    }

    async function remove(id) {
      try {
        await axios.delete(`http://localhost:3000/articles/${id}`);
        articles.value = articles.value.filter((article) => article.id !== id);
        console.log("Article deleted:", id); // Debugging log
      } catch (error) {
        console.error("Error deleting article:", error);
      }
    }

    function edit(article) {
      form.id = article.id;
      form.title = article.title;
      form.content = article.content;
    }

    onMounted(load);

    return { form, articles, save, edit, remove, load };
  },
};
</script>

<style scoped>
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #f0f4f8, #a0c4ff);
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

.form {
  width: 100%;
  max-width: 500px;
  margin-bottom: 20px;
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: fadeInUp 0.5s ease forwards;
}

.input, .textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
}

.button {
  padding: 10px 20px;
  border: none;
  background: linear-gradient(135deg, #007bff, #0056b3);
  color: white;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  transform: translateY(0);
}

.button:hover {
  background: linear-gradient(135deg, #0056b3, #003c7a);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.3);
  transform: translateY(-2px);
}

.button:active {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  transform: translateY(1px);
}

.button.delete {
  background: linear-gradient(135deg, #dc3545, #a71d2a);
}

.button.delete:hover {
  background: linear-gradient(135deg, #a71d2a, #6d1018);
}

.button.edit {
  background: linear-gradient(135deg, #28a745, #1e7e34);
}

.button.edit:hover {
  background: linear-gradient(135deg, #1e7e34, #155d27);
}

.button.load {
  margin-top: 20px;
  background: linear-gradient(135deg, #17a2b8, #117a8b);
}

.button.load:hover {
  background: linear-gradient(135deg, #117a8b, #0a5e6b);
}

.articles-list {
  list-style-type: none;
  padding: 0;
  width: 100%;
  max-width: 600px;
}

.article {
  background-color: white;
  padding: 20px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  animation: fadeInUp 0.5s ease forwards;
}

.article:hover {
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
}

.article-content {
  margin-bottom: 10px;
}

.article-actions {
  display: flex;
  justify-content: flex-end;
}

.article-actions .button {
  margin-left: 10px;
}
</style>
