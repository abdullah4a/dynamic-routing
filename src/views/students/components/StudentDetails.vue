<template>
  <div>
    <div class="students" v-if="student !== undefined">
      Student Id is: <strong>{{ student.id }}</strong>
      <h4>{{ student.name }}</h4>
      <p>
        Email:
        <span>
          <strong>
            {{ student.email }}
          </strong>
        </span>
        <br />
        Phone:
        <span>
          <strong>
            {{ student.phone }}
          </strong>
        </span>
        <br />
        Website:
        <span>
          <strong>
            {{ student.website }}
          </strong>
        </span>
        <br />
        Company Name:
        <span>
          <strong>
            {{ student.company.name }}
          </strong>
        </span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      student: undefined,
    };
  },
  methods: {
    fetchStudent() {
      fetch(
        `https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`
      )
        .then(async (students) => {
          this.student = await students.json();
        })
        .catch((err) => {
          throw err;
        });
    },
  },
  created() {
    this.fetchStudent();
  },
};
</script>

<style scoped>
.students {
  font-size: larger;
  text-align: left;
  margin-left: 42%;
}
</style>