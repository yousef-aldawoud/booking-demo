<template>
  <div>
      <b-modal v-model="open" ref="model" hide-footer title="Using Component Methods">
        <b-form-input class="field-margin"
          v-model="bookingDetails.customerName"
          required
          placeholder="Enter name"
        ></b-form-input>
        <b-form-textarea
        class="field-margin"
            id="textarea"
            v-model="bookingDetails.description"
            placeholder="Description"
            rows="3"
            max-rows="6"
        ></b-form-textarea>
            <date-pick class="field-margin" v-model="bookingDetails.date"></date-pick>
            <div>
                <b-button :variant="colored?'danger':''" class=" button" @click="openDialog()">cancel</b-button>
                <b-button v-if="edit" @click="editItem" :variant="colored?'primary':''" class=" button">Update</b-button>
                <b-button @click="addItem" v-else :variant="colored?'success':''" class=" button">Add</b-button>
            </div>
      </b-modal>
  </div>
</template>
<script>
import DatePick from 'vue-date-pick';
import 'vue-date-pick/dist/vueDatePick.css';

export default {
    components: {DatePick},
    props:{
        colored:{default:false}
    },
    data(){
        return{
            edit:false,
            open:false,
            editIndex:0,
            bookingDetails:{
                customerName:"",date:"2019-10-10",description:""
            },
        }
    },methods:{
        openDialog(edit=false,details={customerName:"",date:"",description:""},index=0){
            console.log("open")
            if(edit){
                this.bookingDetails = details
                this.editIndex = index
                this.edit = true;
            }
            if(this.open){
                this.bookingDetails ={customerName:"",date:"2019-10-10",description:""}
                this.edit = false
                this.editIndex = 0
            }
            
            this.open = !this.open
        },
        editItem(){
            this.$emit("edit-booking",this.bookingDetails,editIndex);
            this.openDialog();
        },addItem(){
            this.$emit("add-booking",this.bookingDetails);
            this.openDialog();
            
        }
    }
}
</script>

<style>
.field-margin{
    margin: 10px;
}
</style>