<template>
   <div>
        <div class="col-md-12 form-wrapper">
          <h2> Create Contact </h2>
          <form id="create-post-form" @submit.prevent="createContact">
               <div class="form-group col-md-12">
                <label for="title"> Name </label>
                <input type="text" id="first_name" v-model="name" name="title" class="form-control" placeholder="Enter firstname">
               </div>

               <div class="form-group col-md-12">
                <label for="title"> Last Name </label>
                <input type="text" id="last_name" v-model="last" name="title" class="form-control" placeholder="Enter Last name">
               </div>

             <div class="form-group col-md-12">
                <label for="title"> Email </label>
                <input type="text" id="email" v-model="email" name="title" class="form-control" placeholder="Enter email">
            </div>
              <div class="form-group col-md-4 pull-right">
                  <button class="btn btn-success" type="submit"> Create Contact </button>
              </div>          
          </form>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import { server } from "../../helper";
import router from "../../router";
export default {
  data() {
    return {
      name: " ",
      last: " ",
      email: " "
    };
  },
  methods: {
    createContact() {
      let contactData = {
        name: this.name,
        last: this.last,
        email: this.email
      };
      this.__submitToServer(contactData);
    },
    __submitToServer(data) {
      axios.post(`${server.baseURL}/api/users`, data).then(data => {
        router.push({ name: "home" });
      });
    }
  }
};
</script>

