<template>
  <div>
      <b-modal v-model="open" ref="model" hide-footer title="Using Component Methods">
        <b-form-input class="field-margin"
          v-model="name"
          required
          placeholder="Enter name"
        ></b-form-input>
        <b-form-textarea
        class="field-margin"
            id="textarea"
            v-model="description"
            placeholder="Description"
            rows="3"
            max-rows="6"
        ></b-form-textarea>
            <input type="date" v-model="date">
            <div>
                <b-button :variant="colored?danger:''" class=" button" @click="openDialog()">cancel</b-button>
                <b-button v-if="edit" @click="editItem" :variant="colored?primary:''" class=" button">Update</b-button>
                <b-button @click="addItem" v-else :variant="colored?success:''" class=" button">Add</b-button>
            </div>
      </b-modal>
  </div>
</template>
<script>

export default {
    props:{
        colored:{default:false},
        randomColor:{default:false},
    },
    data(){
        return{
            success:this.randomColor ? "danger":"success",
            warning:this.randomColor ? "primary":"warning",
            danger:this.randomColor ? "success":"danger",
            primary:this.randomColor ? "warning":"primary",
            name:"",
            description:"",
            date:"2019-01-01",
            edit:false,
            open:false,
            editIndex:0,
            bookingDetails:{
                customerName:"",date:"2019-10-10",description:""
            },
        }
    },methods:{
        openDialog(edit=false,details={customerName:"",date:"",description:""},index=0){
            if(edit){
                this.name = details.customerName
                this.description = details.description
                this.date = details.date
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
            this.bookingDetails.date = this.date;
            this.bookingDetails.customerName = this.name;
            this.bookingDetails.description = this.description;
            this.$emit("edit-booking",this.bookingDetails,this.editIndex);
            this.openDialog();
        },addItem(){
            this.$emit("add-booking",this.bookingDetails);
            this.bookingDetails.date = this.date;
            this.bookingDetails.customerName = this.name;
            this.bookingDetails.description = this.description;
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