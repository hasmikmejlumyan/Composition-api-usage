<template>
  <section class="container">
    <user-data :firstName='firstName' :lastName='lastName'></user-data>
    <button @click='setAge'>Change Age</button>

    <div>
      <input type='text' placeholder='First Name' v-model='firstName' />
      <input type='text' placeholder='Last Name' ref='lastNameInput' />
      <button @click='setLastName'>Set Name</button>
    </div>
  </section>
</template>

<script>
import { ref, computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData,
  },

  setup() {
    // const uName = ref('Hasmik');
    const uAge = ref('26');
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);

    // const user = reactive({
    //   name: 'Hasmik',
    //   age: 26,
    // });

    provide('userAge', uAge);

    const uName = computed(() => {
      return firstName.value + ' ' + lastName.value;
    });

    watch([uAge, uName], (newValue, oldValue) => {
      console.log(oldValue, newValue);
    });

    const setNewAge = () => {
      uAge.value = 27;
    }

    const setLastName = () => {
      lastName.value = lastNameInput.value.value;
    }

    return {
      userName: uName,
      userAge: uAge,
      setAge: setNewAge,
      firstName,
      lastName,
      lastNameInput,
      setLastName,
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