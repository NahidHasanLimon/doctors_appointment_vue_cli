<template>
      <div class="col-12 col-md-10 col-lg-7">
    <div class="input-group my-3">
      <input
        id="SearchApts"
        placeholder="Search"
        type="text"
        class="form-control"
        aria-label="Search Appointments"
        v-model="searchTerm"
      >

      <div class="input-group-append">
        <button
          type="button"
          class="btn btn-primary dropdown-toggle"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          Sort by
          <span class="caret"></span>
        </button>

        <div class="dropdown-menu dropdown-menu-right">
          <a href="#" class="dropdown-item d-flex justify-content-between" id="petName"
           @click="$emit('request-key','petName')"
           >
            Pet Name
            <span class="bg-success"
            v-if="myKey==='petName'" >
            checked</span>
            <!-- <font-awesome-icon icon="check"/> -->
          </a>

          <a class="dropdown-item d-flex justify-content-between" href="#" id="aptDate"
          @click="$emit('request-key','aptDate')">
            Date
            <!-- <font-awesome-icon icon="check"/> -->
            <span class="bg-success"
            v-if="myKey==='aptDate'"
             
            >checked</span>
            
          </a>

          <a href="#" class="dropdown-item d-flex justify-content-between" id="ownerName"
           @click="$emit('request-key','petOwner')">
            Owner
            <span class="bg-success"
            v-if="myKey==='petOwner'"
            >checked</span>
                        <!-- <font-awesome-icon icon="check"/> -->
          </a>

          <div class="dropdown-divider" role="separator"></div>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="asc"
             @click="$emit('request-dir','asc')"
          >
            Asc
            <span class="bg-success"
            v-if="myDir==='asc'"
            >checked</span>
            <!-- <font-awesome-icon icon="check"/> -->
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="desc"
             @click="$emit('request-dir','desc')"
          >
            Desc
            <span class="bg-success"
            v-if="myDir==='desc'">checked</span>
            <!-- <font-awesome-icon icon="check"/> -->
          </a>
        </div>
      </div>
    </div>
  </div>

</template>
<script>

export default {
    name: "SearchAppointment",
    data: function(){
        return {
            searchTerm: "",
        }
    },
    watch:{
        searchTerm:function(){
            this.$emit("search-records",this.searchTerm);
        }
    },
    components:{

        // SearchAppointment,
    },
    props:["myKey","myDir"],
}
</script>>