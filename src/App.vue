<template>
  <section class="container">
    <h2>{{ userName }}</h2>
    <h3>{{ userAge }}</h3>
    <button @click='setAge'>Change Age</button>

    <div>
      <input type='text' placeholder='First Name' v-model='firstName' />
      <input type='text' placeholder='Last Name' v-model='lastName' />
    </div>
  </section>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  setup() {
    // const uName = ref('Hasmik');
    const uAge = ref('26');
    const firstName = ref('');
    const lastName = ref('');

    // const user = reactive({
    //   name: 'Hasmik',
    //   age: 26,
    // });

    const uName = computed(() => {
      return firstName.value + ' ' + lastName.value;
    });

    watch([uAge, uName], (newValue, oldValue) => {
      console.log(oldValue, newValue);
    });

    const setNewAge = () => {
      uAge.value = 27;
    }

    return {
      userName: uName,
      userAge: uAge,
      setAge: setNewAge,
      firstName,
      lastName,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>