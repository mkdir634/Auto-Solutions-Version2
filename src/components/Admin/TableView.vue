<template>
    <div class="p-5 mts">
      <h1 class="text-center fw-bolder">{{ title }}</h1>
  
      <div class="table-responsive">
        <table
          class="table table-dark table-hover"
          :class="{'navbar-dark': isDark, 'navbar-light': !isDark}"
          :style="{ backgroundColor: isDark ? 'rgba(52, 52, 52, 0.8)' : 'rgba(200, 200, 200, 0.8)', color: isDark ? '#fff' : '#333' }"
        >
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Model</th>
              <th scope="col">Year</th>
              <th scope="col">Brand</th>
              <th scope="col">Mileage</th>
              <th scope="col">Engine</th>
              <th scope="col">HorsePower</th>
              <th scope="col">Torque</th>
              <th scope="col">Top Speed</th>
              <th scope="col">Years Owned</th>
              <th scope="col">Price</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(car, index) in cars" :key="car.id">
              <th scope="row">{{ index + 1 }}</th>
              <td>{{ car.model }}</td>
              <td>{{ car.year }}</td>
              <td>{{ car.brand }}</td>
              <td>{{ car.mileage }}</td>
              <td>{{ car.engine }}</td>
              <td>{{ car.horsepower }}</td>
              <td>{{ car.torque }}</td>
              <td>{{ car.topSpeed }}</td>
              <td>{{ car.yearsowned }}</td>
              <td>{{ car.price }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, watch } from 'vue';
  import { supabase } from '../../lib/supaBase';
  

  const props = defineProps({
    title: {
      type: String,
      default: 'Title',
    },
    tableName: {
      type: String,
      required: true, 
    },
    forRent: {
      type: Boolean,
      default: false, 
    }
  });
  

  const cars = ref([]);
  const isDark = ref(false);
  

  const fetchCars = async (table, forRent = false) => {
  const query = supabase.from(table).select('*');
  if (forRent) {
    query.eq('forRent', true); 
  }
  const { data, error } = await query;
  if (error) {
    console.error('Error fetching cars:', error);
  } else {
    cars.value = data;
  }
};


  onMounted(() => {
    fetchCars(props.tableName, props.forRent);
    const savedTheme = localStorage.getItem('theme') || 'light';
    isDark.value = savedTheme === 'dark';
  });
  

  watch(() => [props.tableName, props.forRent], ([newTable, newForRent]) => {
    fetchCars(newTable, newForRent); // Update data based on the new props
  });
  </script>
  
  <style>
  .max {
    max-width: 1100px;
  }
  
  .mts {
    margin-top: 40px;
  }
  </style>
  