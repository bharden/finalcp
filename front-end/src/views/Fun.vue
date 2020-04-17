<template>
<div class="Fun">
  <h1>The Fun Page</h1>
    <div class="heading">
      <h2>Post your favorite sheet music for everyone to use!</h2>
    </div>
  <div class="add">
    <div class="form">
      <input v-model="title" placeholder="Title">
      <br>
      <input v-model="genre" placeholder="Genre">
      <br>
      <input v-model="artist" placeholder="Artist">
      <p></p>
      <input class="choose" type="file" name="music" @change="fileChanged">
      <button @click="upload">Post Music</button>
    </div>
    <div class="upload" v-if="addItem">
      <h2>{{addItem.title}}</h2>
      <img :src="addItem.path" />
    </div>
  </div>
  <div class="heading">
    <div class="circle">2</div>
    <h2>Edit/Delete an Item</h2>
  </div>
  <div class="edit">
    <div class="form">
      <input v-model="findTitle" placeholder="Search">
      <div class="suggestions" v-if="suggestions.length > 0">
        <div class="suggestion" v-for="s in suggestions" :key="s.id" @click="selectItem(s)">{{s.title}}
        </div>
      </div>
    </div>
    <div class="upload" v-if="findItem">
      <input v-model="findItem.title">
      <p></p>
      <img :src="findItem.path" />
    </div>
    <div class="actions" v-if="findItem">
      <button @click="deleteItem(findItem)">Delete</button>
      <button @click="editItem(findItem)">Edit</button>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Fun',
  data() {
  return {
    title: "",
    genre: "",
    artist: "",
    file: null,
    addItem: null,
    items: [],
    findTitle: "",
    findItem: null,
  }
},
created() {
  this.getItems();
},
computed: {
  suggestions() {
    let items = this.items.filter(item => item.title.toLowerCase().startsWith(this.findTitle.toLowerCase()));
    return items.sort((a, b) => a.title > b.title);
  }
},
methods: {
  fileChanged(event) {
    this.file = event.target.files[0]
  },
  selectItem(item) {
    this.findTitle = "";
    this.findItem = item;
  },
  async upload() {
  try {
    const formData = new FormData();
    formData.append('music', this.file, this.file.name)
    let r1 = await axios.post('/api/musics', formData);
    let r2 = await axios.post('/api/items', {
      title: this.title,
      genre: this.genre,
      artist: this.artist,
      path: r1.data.path
    });
    this.addItem = r2.data;
  } catch (error) {
    console.log(error);
  }
},
async deleteItem(item) {
  try {
    await axios.delete("/api/items/" + item._id);
    this.findItem = null;
    this.getItems();
    return true;
  } catch (error) {
    console.log(error);
  }
},
async getItems() {
  try {
    let response = await axios.get("/api/items");
    this.items = response.data;
    return true;
  } catch (error) {
    console.log(error);
  }
},
async editItem(item) {
  try {
    await axios.put("/api/items/" + item._id, {
      title: this.findItem.title,
      genre: this.findItem.genre,
      artist: this.finItem.artist,
    });
    this.findItem = null;
    this.getItems();
    return true;
  } catch (error) {
    console.log(error);
  }
},
}
}
</script>

<style scoped>
.image h2 {
  font-style: italic;
  font-size: 1em;
}

.heading {
  text-align: center;
  margin-bottom: 20px;
  margin-top: 20px;
}

.heading h2 {
  text-align: center;
  margin-top: 8px;
}

.add,
.edit {

}

/* Form */
input,
textarea,
select,
button {
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-size: 1em;
}
button {
  background: linear-gradient(-90deg, #f2e6ff, #809fff);
}
input {
  margin: 2.5px
}
.form {
  text-align: center;
}

/* Uploaded images */
.upload h2 {
  margin: 0px;
}

.upload img {
  max-width: 300px;
}
/* Suggestions */
.suggestions {
  margin-left: auto;
  margin-right: auto;
  width: 200px;
  border: 1px solid #ccc;
}

.suggestion {
  min-height: 20px;
}

.suggestion:hover {
  background-color: #5BDEFF;
  color: #fff;
}
</style>
