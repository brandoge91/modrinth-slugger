<script setup>
const slug = useState("slug");
const msg = useState("msg");

const base = "https://api.modrinth.com/v2"

function search() {
  if (!slug.value) {
    msg.value = "Please enter a project slug";
    return;
  }
  msg.value = "Searching...";

  const request = $fetch(`${base}/project/${slug.value}`);

  request
    .then((response) => {
      if (response.downloads) {
        msg.value = response.downloads + " Downloads"
      } else {
        msg.value = "Not Found!";
      }
    })
    .catch((error) => {
      msg.value = "Not Found!";
    });
}
</script>

<template>
  <div>
    <h1>Modrinth Search</h1>
    <div>
      <input type="text" v-model="slug" placeholder="Project Slug" />
      <button @click="search">Search</button>
      <p>{{ msg }}</p>
    </div>
  </div>
</template>
