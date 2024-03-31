<template>
  <v-app :theme="theme">
    <v-app-bar app>
      <v-toolbar-title>Travel App</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'" @click="onToggleTheme">
        Toggle Theme
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container fluid>
        <h2>Attractions</h2>
        <v-row dense>
          <v-col 
            v-for="item in items"
            :key="item.id"
            cols="12" sm="4"
          >
            <v-card>
              <v-img
                :src="item.coverimage" 
                height="200px"
                class="align-end"
                cover
              >
                <v-card-title>{{ item.name }}</v-card-title>
              </v-img>
              <v-card-text>{{ item.detail }}</v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
//We can use onMounted or Fetch for get the data
import { ref, onMounted } from 'vue';

const theme = ref('light');
const items = ref([]);

const onToggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light';
};

onMounted(() => {
  fetch('https://www.melivecode.com/api/attractions')
    .then(res => res.json())
    .then(result => {
      items.value = result;
      console.log(result);
    });
});
</script>
