<template>
  <div>
    <h1>My CRUD App</h1>
  <ul>
      <li v-for="(item, index) in items" :key="index">
        <div class="item-info">
          {{ item.name }}
        </div>
        <div class="item-buttons">
          <button @click="editItem(index)">Edit</button>
          <button @click="deleteItem(index)">Delete</button>
        </div>
      </li>
    </ul>

    <!-- Edit Form -->
    <div v-if="editingItem !== null">
      <h2>Edit Item</h2>
      <form @submit.prevent="updateItem">
        <input v-model="editedItem.name" type="text" />
        <div class="save-button">
        <button type="submit">Save</button>

        <button @click="cancelEdit">Cancel</button>
      </div>
      </form>
    </div>

    <!-- Add Item Form -->
    <form @submit.prevent="addItem">
      <input v-model="newItem" type="text" placeholder="New Item" />
      <button type="submit">Add Item</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: "Item 1" },
        { name: "Item 2" },
        // ...more items
      ],
      newItem: "",
      editingItem: null,
      editedItem: { name: "" },
    };
  },
  methods: {
    addItem() {
      if (this.newItem.trim() !== "") {
        this.items.push({ name: this.newItem });
        this.newItem = "";
      }
    },
    editItem(index) {
      this.editingItem = index;
      this.editedItem.name = this.items[index].name;
    },
    updateItem() {
      if (this.editedItem.name.trim() !== "") {
        this.items[this.editingItem].name = this.editedItem.name;
        this.cancelEdit();
      }
    },
    cancelEdit() {
      this.editingItem = null;
      this.editedItem.name = "";
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
  },
};
</script>

<style scoped>

/* Reset some default styles */
* {
  margin: 20px;
  padding: 10px;
  box-sizing: border-box;
}
h1{
  text-align: center;
}

/* Body styles */
body {
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* Container styles */
.container {
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 400px;
  text-align: center;
}

h1 {
  font-size: 28px;
  color: #333;
  margin-bottom: 20px;
}

/* List styles */
ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #e0e0e0;
  color: #555;
}

.item-info {
  flex: 1;
}

.item-buttons {
  display: flex;
  gap: 10px; /* Adds spacing between buttons */
}
/* Edit form styles */
.save-button{
  display: flex;
  gap: 10px;
}
form {
  display: flex;
  flex-direction: column; /* Stack input elements vertically */
  margin-top: 20px;
}

input[type="text"] {
  padding: 8px;
  border: 1px solid #e0e0e0;
  border-radius: 3px;
  margin-bottom: 10px;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 103px;
  padding: 8px 16px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

/* Add Item form styles */
form:first-child {
  margin-bottom: 120px;
}

</style>
