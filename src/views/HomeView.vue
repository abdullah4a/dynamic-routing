<template>
  <div class="home">
    <button
      class="btn"
      v-for="(student, index) in students"
      :key="index"
      @click="goto(student.id)"
    >
      {{ student.name }}
    </button>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data(){
    return {
      students:undefined
    };
  },
  methods: {
    goto(id) {
      // Dynamic routing
      this.$router.push({ name: "studentDetails", params: { id } });
    },
    fetchStudents(){
      fetch("https://jsonplaceholder.typicode.com/users").then(async students=>{
      this.students=await students.json()
      this.students=this.students.map(student=>({name:student.name, email:student.email, id:student.id, phone:student.phone}))
    }).catch(err=>{
      throw err
    })
    }
  },
  created() {
    this.fetchStudents()
  },
};
</script>

<style scoped>
.btn {
  margin: 10px;
  padding: 2%;
  border: none;
  background: black;
  color: aliceblue;
  font-size: larger;
}
.btn:hover {
  margin: 10px;
  padding: 2%;
  border: none;
  background: black;
  color: aliceblue;
  box-shadow: 6px 10px rgba(32, 32, 32, 0.582);
}
</style>