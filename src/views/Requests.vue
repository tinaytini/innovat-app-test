<template>
  <div class="requests">
    <h1>Запросы обратной связи</h1>
    <ul>
      <li v-for="(request, idx) in requests" :key="idx">
        <span>FirstName: {{ request.firstName }}</span>
        <span>LastName: {{ request.lastName }}</span>
        <span>Phone number: {{ request.phoneNumber }}</span>
        <span>Email: {{ request.email }}</span>
      </li>
    </ul>
    <h1>Запросы доставки</h1>
    <ul>
      <li v-for="(request, idx) in calculatedRequests" :key="idx">
        <span>From: {{ request.from }}</span>
        <span>To: {{ request.to }}</span>
        <span>Weight: {{ request.weight }}</span>
        <span>Price: {{ request.price }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Requests',
  data() {
    const requests = localStorage.getItem('requests');
    const calculatedRequests = localStorage.getItem('calculated_requests');

    return {
      requests: requests ? JSON.parse(requests) : [],
      calculatedRequests: calculatedRequests ? JSON.parse(calculatedRequests) : [],
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
span {
  margin: 5px;
}
.requests ul {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-direction: column;
  list-style-type: none;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
}
.requests li {
  text-align: left;
  width: 100%;
  margin-bottom: 15px;
  padding-bottom: 10px;
  border-bottom: 1px solid #42b983;
}
</style>
