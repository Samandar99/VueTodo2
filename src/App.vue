<template>
  <div class="conatiner">
    <Sidebar />
    <h1 class="title">Задачи отсутствуют</h1>
  </div>
</template>

<script>
import Sidebar from "@/components/Sidebar.vue";
export default {
  components: {
    Sidebar,
  },
};
</script>

<style scoped>
.title {
  color: #c9d1d3;
  font-weight: 700;
  font-size: 32px;
  font-family: 'Montserrat';
 
}

.conatiner {
  display: flex;
  
}
</style>


