<template>
  <tr v-bind:class="{ present: student.present, absent: !student.present }">    
    <td>{{ student.name }}</td>
    <td>{{ student.starID }}</td>
    <td><input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedOrLeft(student, $event.srcElement.checked)"></td>
    <td v-show="edit"> <img v-on:click="deleteStudent" src="delete.png"> </td>
  </tr>
</template>



<script>
export default {
    name: 'StudentRow',
    props: {
        student: Object,
        edit: Boolean
    },
    methods: {
        arrivedOrLeft(student, present) {
            this.$emit('student-arrived-or-left', student, present)
        },
        deleteStudent() {
            if (confirm(`Delete ${this.student.name}?`)) {
                this.$emit('delete-student', this.student)
            }
        }
    }
}
</script>


<style  scoped>

.present {
    color: darkgreen;
    font-style: italic;
    background-color: darkorange;
}

.absent {
    color: black;
    font-weight: bold;
    background-color: darkviolet;
}

/*icon height */
img {
    height: 25px;
}

</style>