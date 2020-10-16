<template>
  <h3 v-if="loading">Loading...</h3>
  <h3 v-if="sent">Отправлено!✅</h3>
  <form v-if="!loading" class="form">
    <h1>Форма расчёта себестоимости доставки</h1>
    <li v-for="(input, idx) in inputs" :key="input.name">
      <input
        :type="input.type"
        :placeholder="input.placeholder"
        v-model="inputs[idx].value"
        required
      />
    </li>
    <button @click.prevent="calculateData">Рассчитать стоимость</button>
    <div class="result">Cтоимость: {{result}}</div>
    <button @click.prevent="handleSubmit">Отправить заявку</button>
  </form>
</template>

<script>
export default {
  name: 'CalculateForm',
  data() {
    return {
      inputs: [
        { name: 'cityFrom', value: '', type: 'text', placeholder: 'Укажите город отправки' },
        { name: 'cityTo', value: '', type: 'text', placeholder: 'Укажите город доставки' },
        { name: 'weight', value: '', type: 'number', placeholder: 'Вес груза(25kg)' },
        { name: 'capacity', value: '', type: 'text', placeholder: 'Объем' },
      ],
      loading: false,
      sent: false,
      result: 0,
    }
  },
  methods: {
    calculateData() {
      const additionalCost = 150;
      this.result = (this.inputs[2].value * this.inputs[3].value) + additionalCost;
    },
    handleSubmit() {
      this.loading = true;
      this.sent = false;
      setTimeout(() => {
        const requests = localStorage.getItem('calculated_requests');
        const requestsList = requests ? JSON.parse(requests) : [];
        requestsList.push({ from: this.inputs[0].value, to: this.inputs[1].value, weight: this.inputs[2].value, price: this.result });
        localStorage.setItem('calculated_requests', JSON.stringify(requestsList));
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

button {
    margin: 10px;
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
