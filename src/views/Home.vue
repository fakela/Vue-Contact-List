<template>
    <div class="container-fluid">

      <div class="text-center">
  

       <div v-if="contact.length === 0">
            <h2> No contact found at the moment </h2>
        </div>
      </div>
       
      <!-- <div class="row"> -->
        <div>
            <table class="table table-bordered">
              <thead class="thead-dark">
                <tr>
                  <th scope="col">Firstname</th>
                  <th scope="col">Lastname</th>
                  <th scope="col">Email</th>
                  <th scope="col">Avatar</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(contact, index) in contact" :key="index">
                  <td>{{ contact.first_name }}</td>
                  <td>{{ contact.last_name }}</td>
                  <td>{{ contact.email }}</td>
                  <td>
                    <img :src="contact.avatar" width="50" height="50">
                    </td>
                  <td>
                    <div class="d-flex justify-content-between align-items-center">
                                <div class="btn-group" style="margin-bottom: 20px;">
                                  <router-link :to="{name: 'Edit', params: {id: contact._id}}" class="btn btn-sm btn-outline-secondary">Edit contact </router-link>
                                  <button class="btn btn-sm btn-outline-secondary" v-on:click="deletecontact(contact._id)">Delete contact</button>
                                </div>
                              </div>
                  </td>
                </tr>
                  <tr v-if="contact.length" v-observe-visibility="handledScrolledToBottom"></tr>
              </tbody>
            </table>
          </div>
      <!-- </div> -->
    </div>
</template>

<script>
import { server } from "../helper";
import axios from "axios";

export default {
  data() {
    return {
      contact: [],
      page: 1
    };
  },
  created() {
    this.fetchContact();
  },
  methods: {
    fetchContact() {
      axios
        .get(`${server.baseURL}/api/users?page=${this.page}`)
        .then(data => {
          // this.contact = data.data.data
          this.contact.push(...data.data.data)
          console.log(this.contact);
          
    });
    },
    deletecontact(id) {
      axios
        .delete(`${server.baseURL}/api/users/2`)
        .then(data => {
          console.log(data);
          window.location.reload();
        });
    },
    handledScrolledToBottom (isvisible){
      if (!isvisible) {return}

      this.page++
      this.fetchContact()
    }
  },

  mounted () {
    this.fetchContact()
  }
};
</script>

