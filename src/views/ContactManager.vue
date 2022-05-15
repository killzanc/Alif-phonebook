

<template>
<div class="container mt-3">
  <div class="row">
    <div class="col">
      <p class="h3 text-success fw-bold">Contact
      <router-link to="/contacts/add" class="btn btn-success btn-sm">New</router-link>
      </p>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Culpa, quidem eos fugit commodi molestias, vero blanditiis deserunt debitis distinctio cum, dicta sapiente beatae porro quibusdam! Doloribus alias commodi illum quos.</p>
      <form>
        <div class="row">
          <div class="col-md-6">
            <div class="row">
              <div class="col">
            <input type="text" class="form-control" placeholder="Search">
              </div> 
              <div class="col">
            <input type="submit" class="btn btn-outline-dark">
          </div>
            </div>
          </div>
         
        </div>
      </form>
    </div>
  </div>
</div>
<div class="container mb-5 mt-3" v-if="contacts.length > 0">
  <div class="row">
    <div class="col-md-6" v-for="contact of contacts" :key="contact">
      <div class="card my-2 list-group-item-success" >
        <div class="card-body">
          <div class="row">
            <div class="col-sm-7">
              <ul class="list-group">
                <li class="list-group-item">Name: <span class="fw-bold">{{contact.name}}</span></li>
                <li class="list-group-item">Number: <span class="fw-bold">{{contact.number}}</span></li>
                <li class="list-group-item">Email: <span class="fw-bold">{{contact.email}}</span></li>
                <li class="list-group-item">Address: <span class="fw-bold">{{contact.address}}</span></li>
              </ul>
            </div>
            <div class="col-sm-4 d-flex flex-column justify-content-center align-center">
              <router-link :to="`/contacts/view/${contact.id}`" class="btn btn-warning my-1">View <i class="fa fa-eye"></i></router-link>
              <router-link :to="`/contacts/edit/${contact.id}`" class="btn btn-primary my-1">Edit <i class="fa fa-pen"></i></router-link>
              <button class="btn btn-danger my-1" @click="clickDeleteContact(contact.id)">Delete <i class="fa fa-trash"></i></button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>


<script>
import {ContactService} from "../sevices/ContactService";

export default {
  name: 'ContactManger',
  data: function(){
    return{
      contacts: [],
      errorMessage: null
    }
  },
  created: async function (){
    try {
      let response = await ContactService.getAllContacts();
      this.contacts = response.data;
    } catch (error) {
      this.errorMessage = error;
    }
  },
  methods: {
    clickDeleteContact: async function(contactId){
      try {
        let response = await ContactService.deleteContact(contactId);
        if(response){
          let response = await ContactService.getAllContacts();
          this.contacts = response.data;
        }
      } catch (error) {
             this.errorMessage = error;
      }
    }
  }
}
</script>


<style>

</style>

