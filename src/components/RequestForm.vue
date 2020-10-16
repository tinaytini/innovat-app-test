<template>
  <h3 v-if="loading">Loading...</h3>
  <h3 v-if="sent">Отправлено!✅</h3>
  <h3 v-if="error">Пожалуйста, заполните все поля</h3>
  <form v-if="!loading" class="form">
    <h1>Форма обратной связи</h1>
    <li v-for="(input, idx) in inputs" :key="input.name">
      <input
        :type="input.type"
        :placeholder="input.placeholder"
        v-model="inputs[idx].value"
        required
      />
    </li>
    <button @click.prevent="handleSubmit">Отправить</button>
  </form>
</template>

<script>
export default {
  name: 'RequestForm',
  data() {
    return {
      inputs: [
        { name: 'firstName', value: '', type: 'text', placeholder: 'Имя' },
        { name: 'lastName', value: '', type: 'text', placeholder: 'Фамилия' },
        { name: 'phoneNumber', value: '', type: 'number', placeholder: 'Номер телефона (0700222333)' },
        { name: 'email', value: '', type: 'email', placeholder: 'Почта' },
      ],
      error: false,
      loading: false,
      sent: false,
    }
  },
  methods: {
    handleSubmit() {
      this.loading = true;
      this.sent = false;

      setTimeout(() => {
        const requests = localStorage.getItem('requests');
        const requestsList = requests ? JSON.parse(requests) : [];
        const newRequest = this.inputs.reduce((acc, { name, value }) => {
          acc[name] = value;
          return acc;
        }, { });

        requestsList.push(newRequest);

        localStorage.setItem('requests', JSON.stringify(requestsList));

        this.loading = false;
        this.sent = true;
      }, 2000);
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.form input {
  width: 100%;
  max-width: 350px;
  margin-bottom: 15px;
  padding: 5px 15px;
  border-radius: 3px;
  border-color: #42b983;
}

.form > button {
  padding: 7px 15px;
  color: #fff;
  background-color: #42b983;
  border-radius: 3px;
  border: 1px solid transparent;
  cursor: pointer;
  transition: .3s;
}
.form > button:hover {
  color: #42b983;
  background-color: #fff;
  border-color: #42b983;
}
</style>
