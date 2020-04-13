<template>
  <div id="employee-table" class="container">
    <p v-if="employees.length<1">No Employees</p>  
    <table v-else>
      <thead>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing === employee.id" >
              <input type="text" v-model="employee.name" />
          </td>
          <td v-else>{{ employee.name }}</td>
          <td v-if="editing===employee.id">
              <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{ employee.email }}</td>
          <td v-if="editing===employee.id">
              <button @click="editEmployee(employee)">Save</button>
              <button @click="editing=null" class="muted-button">Cancel</button>
          </td>
          <td v-else>
              <button @click="editMode(employee.id)">Edit</button>
              <button @click="$emit('delete:employee',employee.id)">Delete</button>
          </td>          
        </tr>
      </thead>
      <tbody>
        <tr>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'employee-table',
  props: {
    employees: Array,
  },
  data(){
      return{
          editing:null
      }
  },
  methods:{
      editMode(id){
          this.editing = id
      },
      editEmployee(employee){
          if(employee.name === '' || employee.email==='')return
          this.$emit('edit:employee', employee.id, employee)
          this.editing = null
      }
  }
}

</script>



<style scoped>
button{
  margin: 0 0.5rem 0 0;
}
.holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input{
    width:calc(100%-40px);
    border:0;
    padding:20px;
    font-size: 1.3em;
    background-color: rgba(250, 250, 36, 0.863) ;
    color:#333f7f;
  }
</style>