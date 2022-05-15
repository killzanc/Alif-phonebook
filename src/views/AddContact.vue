<template>
  <div class="container mt-3">
    <div class="row">
      <div class="col">
        <p class="h3 text-success fw-bold">Add Contact</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Eos esse laborum qui, sapiente aut eveniet saepe optio ab maiores dolorum perferendis est odio, enim vitae voluptatum possimus dignissimos reprehenderit placeat.</p>
      </div>
    </div>
  </div>
  <div class="container mt-3">
    <div class="row">
      <div class="col-md-3">
        <form @submit.prevent="submitCreate()">
          <div class="mb-2">
            <input v-model="contact.name" type="text" class="form-control" placeholder="Name">
          </div>
          <div class="mb-2">
            <input v-model="contact.number" type="number" class="form-control" placeholder="Number">
          </div>
          <div class="mb-2">
            <input v-model="contact.email" type="email" class="form-control" placeholder="Email">
          </div>
          <div class="mb-2">
            <input v-model="contact.address" type="text" class="form-control" placeholder="Address">
          </div>
          <div class="mb-2">
            <input type="submit" class="btn btn-success" value="Create">
          </div>
        </form>
      </div>
    </div>
  </div>
</template>


<script>
import { ContactService } from '@/sevices/ContactService'
export default {
  name: 'AddContact',
  data: ()=>{
    return{
      contact:{
        name : '',
        number : '',
        email : '',
        address : ''
      }
    }
  },
  methods :{
    submitCreate: async function(){
      try {
        let response = await ContactService.createContact(this.contact)
        if (response) {
          return this.$router.push('/');
        } else {
          return this.$router.push('/contacts/add')
        }
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script> 


<style>

</style>

