<template>
    <b-card>
        <b-card-text>
            <h4>Customer name :- {{customerName}}</h4> 
            <strong>Room number</strong>
            <p>
                {{description}}
            </p>
        </b-card-text>

        <b-card-text>
            <strong>Booking date:-</strong> {{bookingDate}}
        </b-card-text>
        <b-button :variant="colored?danger:''" class=" button" @click="deleteBooking">delete</b-button>
        <b-button @click="edit" :variant="colored?primary:''" class=" button">edit</b-button>
    </b-card>
</template>

<script>
export default {
    props:{
        colored:{default:false},
        randomColor:{default:false},
        description:{default:""},
        bookingDate:{default:""},
        customerName:{default:""},
    },
    data(){
        return{

        success:this.randomColor ? "warning":"success",
        warning:this.randomColor ? "success":"warning",
        danger:this.randomColor ? "primary":"danger",
        primary:this.randomColor ? "danger":"primary",

        }
    },methods:{
        edit(){
            this.$emit("edit")
        },deleteBooking(){
            this.$emit("delete-booking")            
        }
    }
}
</script>
<style>
.button{
    margin: 10px;
}
</style>