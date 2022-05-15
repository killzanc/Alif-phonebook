

<template>
  <div class="container mt-3">
    <div class="row">
      <div class="col">
        <p class="h3 text-success fw-bold">View contact</p>
        <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Earum, provident! Neque saepe, rem minus ad soluta velit dolores! Unde accusantium ea voluptas aperiam nam odio voluptatem obcaecati laudantium architecto quibusdam?</p>
      </div>
    </div>
  </div>

  <div class="container" v-if="isDone()">
    <div class="row">
      <div class="col-md">
        <ul class="list-group">
                <li class="list-group-item">Name: <span class="fw-bold">{{contact.name}}</span></li>
                <li class="list-group-item">Number: <span class="fw-bold">{{contact.number}}</span></li>
                <li class="list-group-item">Email: <span class="fw-bold">{{contact.email}}</span></li>
                <li class="list-group-item">Address: <span class="fw-bold">{{contact.address}}</span></li>
              </ul>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <router-link to="/" class="btn btn-success mt-3">Back</router-link>
      </div>
    </div>
  </div>
</template>


<script>
import { ContactService } from '@/sevices/ContactService'
export default {
  name: 'ViewContact',
  data:function () {
    return{
      contactId: this.$route.params.contactId,
      contact: {},
      errorMessage: null
    }
  },
  created:async function () {
    try {
    let response = await ContactService.getContact(this.contactId);
      this.contact = response.data
    } catch (error) {
      this.errorMessage = error
    }
  },
  methods: {
    isDone: function(){
    return Object.keys(this.contact).length > 0;
  }
}
}
</script>


<style>

</style>

