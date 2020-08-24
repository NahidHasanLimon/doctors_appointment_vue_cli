<template>
      <div class="col-12 mb-5">
    <div class="card textcenter mt-3">
      <div class="card-header bg-primary text-white">
        <!-- <font-awesome-icon icon="plus" class="mr-3"/>Add Appointment -->
      <button class="btn  btn-sm btn-success bg-dark"
        @click="hidepanel=!hidepanel"
      >+
      </button>
      </div>

      <div class="card-body" :class="{'d-none':hidepanel}"> 
        <form id="aptForm"
        @submit.prevent ="requestAdd">
          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="aptName">Pet Name</label>
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                name="aptName"
                id="aptName"
                placeholder="Pet's Name" required=""
                v-model="formData.petName"
              >
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="petOwner">Pet Owner</label>
            <div class="col-md-10">
              <input type="text" class="form-control" id="petOwner" placeholder="Owner's Name"
                v-model="formData.petOwner">
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="aptDate">Date</label>
            <div class="col-md-4">
              <input type="date" class="form-control" id="aptDate"
               v-model="formData.aptDate">
            </div>
            <label class="col-md-2 col-form-label text-md-right" for="aptTime">Time</label>
            <div class="col-md-4">
              <input type="time" class="form-control" name="aptTime" id="aptTime"
              v-model="formData.aptTime">
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 text-md-right" for="aptNotes">Apt. Notes</label>
            <div class="col-md-10">
              <textarea
                class="form-control"
                rows="4"
                cols="50"
                name="aptNotes"
                id="aptNotes"
                v-model="formData.aptNotes"
                placeholder="Appointment Notes"
              ></textarea>
            </div>
          </div>

          <div class="form-group form-row mb-0">
            <div class="offset-md-2 col-md-10">
              <button type="submit" class="btn btn-primary d-block ml-auto">Add Appointment</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>

// import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome"
export default {
    name: "AddAppointment",
    data: function (){
         return {
             formData: [],
             hidepanel: true,
         }
    },
    components:{
        // FontAwesomeIcon,
    },
    methods:{
        
        requestAdd :  function(){
            // alert(this.formData);
            this.formData={
                petName: this.formData.petName,
                petOwner: this.formData.petOwner,
                aptDate: this.formData.aptDate + ' '+ this.formData.aptTime,
                aptNotes: this.formData.aptNotes,
            };
            console.log(this.formData);
            this.$emit("add",this.formData);
            this.formData=[];
            this.hidepanel=true;
        }
    },
}
</script>
