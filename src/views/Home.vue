<template>
  <div class="home">
    <RequestForm />
    <CalculateForm />
  </div>
</template>

<script>
import RequestForm from '@/components/RequestForm.vue'
import CalculateForm from '@/components/CalculateForm.vue'

export default {
  name: 'Home',
  components: {
    RequestForm,
    CalculateForm
  }
}
</script>
