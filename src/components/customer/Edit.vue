<template>
   <div>
        <h4 class="text-center mt-20">
         <small>
         <button class="btn btn-success" v-on:click="navigate()"> View All contacts </button>
         </small>
        </h4>

        <div class="col-md-12 form-wrapper">
          <h2> Edit contact </h2>
          <form id="create-post-form" @submit.prevent="editcontact">
               <div class="form-group col-md-12">
                <label for="title"> First Name </label>
                <input type="text" id="first_name" v-model="contact.first_name" name="title" class="form-control" placeholder="Enter firstname">
               </div>

               <div class="form-group col-md-12">
                <label for="title"> Last Name </label>
                <input type="text" id="last_name" v-model="contact.last_name" name="title" class="form-control" placeholder="Enter Last name">
               </div>

             <div class="form-group col-md-12">
                <label for="title"> Email </label>
                <input type="text" id="email" v-model="contact.email" name="title" class="form-control" placeholder="Enter email">
            </div>


              <div class="form-group col-md-4 pull-right">
                  <button class="btn btn-success" type="submit"> Edit contact </button>
              </div>          
          </form>
        </div>
    </div>
</template>

<script>
import { server } from "../../helper";
import axios from "axios";
import router from "../../router";
export default {
  data() {
    return {
      id: 0,
      contact: {}
    };
  },
  created() {
    this.id = this.$route.params.id;
    this.getContact();
  },
  methods: {
    editContact() {
      let contactData = {
        first_name: this.contact.first_name,
        last_name: this.contact.last_name,
        email: this.contact.email
      };

      axios
        .put(
          `${server.baseURL}/api/users`,
          contactData
        )
        .then(data => {
          router.push({ name: "home" });
        });
    },
    getContact() {
      axios
        .get(`${server.baseURL}/api/users`)
        .then(data => (this.contact = data.data));
    },
    navigate() {
      router.go(-1);
    }
  }
};
</script>

