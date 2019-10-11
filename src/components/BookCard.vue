<template>
    <b-card>
        <b-card-text>
            <h4>Customer name :- {{customerName}}</h4> 
            <strong>Description</strong>
            <p>
                {{description}}
            </p>
        </b-card-text>

        <b-card-text>
            <strong>Booking date:-</strong> {{bookingDate}}
        </b-card-text>
        <b-button :variant="colored?'danger':''" class=" button">delete</b-button>
        <b-button @click="edit" :variant="colored?'primary':''" class=" button">edit</b-button>
    </b-card>
</template>

<script>
export default {
    props:{
        colored:{default:false},
        description:{default:""},
        bookingDate:{default:""},
        customerName:{default:""},
    },
    data(){
        return{

        }
    },methods:{
        edit(){
            this.$emit("edit")
        }
    }
}
</script>
<style>
.button{
    margin: 10px;
}
</style>