<template>
  <div id="main-app">
    <div class="container">
      <AddAppointment @add="addItem" />
      <SearchAppointment 
      @search-records="searchAppointments" 
      :myKey="filterKey"
      :myDir="filterDir"
      @request-dir="changeDir"
      @request-key="changeKey"
        />
      
      <div class="row justify-content-center">
        <appointment-list v-bind:appointments="filteredApts" @remove="removeItem" @edit="editItem"/>
      </div>
  </div>
     <!-- <font-awesome-icon
            :icon="plus"
    ></font-awesome-icon> -->
  </div>
</template>

<script>
// import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import axios from "axios";
import AppointmentList from "./components/AppointmentList";
import AddAppointment from "./components/AddAppointment";
import SearchAppointment from "./components/SearchAppointment";
import _ from "lodash";


export default {
  name: "MainApp",
  data: function(){
    return {
      title:"Appointment List",
      appointments: [],
      aptIndex:0,
      searchTerms:[],
      filterKey:"petName",
      filterDir:"asc",

    };
  },
  components: { 
    // FontAwesomeIcon,
    AppointmentList,
    AddAppointment,
    SearchAppointment,

  },
  computed:{
    searchedApts:function(){
      console.log(this.searchTerms);
      return this.appointments.filter( item => {
        return(
          // item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          // item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          // item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase()) 
        item.aptNotes
       );
      });
    },
    filteredApts:function () {
      return _.orderBy(
        this.searchedApts,
        item => {
          return item[this.filterKey].toLowerCase();
        },this.filterDir
      )
    }
  },
  methods:{
    removeItem:function(apt){
      this.appointments= _.without(this.appointments,apt);
      console.log(this.appointments);
    },
    editItem: function(id,field,text){
      const aptIndex = _.findIndex(this.appointments,
      {
        aptId:id
      });
      this.appointments[aptIndex][field]=text;
         console.log(this.appointments[0].petOwner);
    },
    addItem: function(apt){
     
      apt.aptId= this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);

    },
    searchAppointments: function(terms){
      this.searchTerms=terms;
    },
    changeKey: function (val){
      this.filterKey=val;
          //  alert();
    },
     changeDir: function (val){
      //  alert();
      this.filterDir=val;
    }
  },
  mounted(){
    axios.get("./data/appointments.json")
    .then(
      response => (
        this.appointments=response.data.map( item => {
          item.aptId=this.aptIndex;
          this.aptIndex++;
          return item;
        }) )
        );
  }
};
</script>

