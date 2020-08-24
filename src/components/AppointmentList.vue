<template>
      <div class="col-12 col-md-10 col-lg-7">
            <div class="card-header text-center">
                <h1>AppointmentList</h1>
            </div>
            <div class="list-group list-group-flush">
                <div class="list-group-item" v-for="item in appointments" v-bind:key="item.aptIndex">
                <button class="mr-2 btn btn-sm btn-danger" @click="$emit('remove',item)">Delete</button>
                        <div class="d-flex justify-content-between">
                            <span class="h4 text-success"
                                contenteditable="true"
                                @blur="$emit('edit',item.aptId,'petName',$event.target.innerText)"
                            >{{item.petName}}</span>
                            <span class="foat-right text-success">{{formattedDate(item.aptDate)}}</span>

                        </div>
                         <div class="owner-name">
                            <span class="float-weight-bold text-primary">Owner:</span>
                            <span 
                            contenteditable="true"
                             @blur="$emit('edit',item.aptId,'petOwner',$event.target.innerText)"
                            >{{item.petOwner}}</span>
                        </div>
                        <div>
                            {{item.aptNotes}}
                        </div>
    
                    
                </div>
        </div>
     </div>
</template> 
<script>
import moment from 'moment';
export default {
    name: "AppointmentList",
    props:["appointments"],
    components:{

    },
    methods:{
        formattedDate:function(date){
            return moment(new Date(date)).format("MM-DD-YY, h:mm a");
        }
    }
      
    

}
</script>