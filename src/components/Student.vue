
<template>
<div class="container">
  <input type="text" v-model="search" placeholder="Search by name">
   <div class="content" v-for="student in filterName " v-bind:key="student.id">
      <img class="image" :src="student.pic" alt="">
      <div class="student-info">
          <h1 class="info">{{student.firstName +" "+ student.lastName}}</h1>
          <div class="infomation">
            <p class="cop">{{ student.company }}</p>
            <p class="ski">{{ student.skill }}</p>
            <p class="email">{{ student.email }}</p>
            <p class="grade">{{ student.grades }}</p>
          </div>
      </div>
  </div>
</div>
</template>

<script>

import axios from "axios";
export default {
  name: "Student.vue",
  data() {
    return {
      students: '',
      search: ''
    }
  },
  mounted() {
    axios
        .get('https://api.hatchways.io/assessment/students')
        .then((res) => {
          this.students = (res.data.students)
        })
  },
  computed:{
    filterName:function (){
      return this.students.filter((student) => {
        return student.company.match(this.search)
      })
    }
  },
  // computed :{
  //   filterName:function (){
  //     return this.info.filter((student)=>{
  //       return student.company.matcth(this.search);
  //     })
  //   }
  // }
}
</script>

<style scoped>
.container{
  margin: auto;
  background-color: #fff;
  width:70%;
  max-height: 80vh;
  border-radius: 12px;
  overflow-y: auto;
  box-shadow: 0 1px 5px rgba(0,0,0,0.2);
}
.content{
  border-bottom:1px solid #dcdcdc;
  display: flex;
  padding-left: 30px;
}
.info{
  font-size: 1.5rem;
  font-weight: 700;
  text-transform: uppercase;
  color: #000;
}
.image{
  width: 120px;
  height: 120px;
  border-radius: 50%;
  border: 1px solid black;
  margin-right: 20px;
  margin-top: 15px;
}
</style>