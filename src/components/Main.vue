<template>
  <b-container >
      <booking-dialog v-on:add-booking="addItem" v-on:edit-booking="doEditItem" ref="booking_model" :colored="colored"></booking-dialog>
      <b-button @click="openDialog" class="booking-card" size="lg" :variant="colored?'success':''">Add new booking</b-button>
    <b-alert v-if="bookings.length ===0" show :variant="colored?'warning':''">There are no bookings to list</b-alert>
      <book-card v-for="(booking,index) in bookings" :key="index" class="booking-card"
                :colored="colored"
                :description="booking.description" :booking-date="booking.date"
                :customer-name="booking.customerName" v-on:delete-booking="deleteItem(index)"
                v-on:edit="editItem(index)"
      />
  </b-container>
</template>

<script>
import BookCard from './BookCard.vue'
import BookingDialog from './BookingDialog.vue'
export default {
    props:{
        colored:{default:false}
    },
  components: {
    BookCard,BookingDialog
  },data(){
      return{
          bookings:[
              {date:"2019-11-19",description:"a couple with a one child",customerName:"Zammel"},
              {date:"2019-11-19",description:"a couple with a one child",customerName:"Zammel"},
          ]
      }
  },methods:{
      openDialog(){
          this.$refs.booking_model.openDialog();    
      },addItem(item){
          this.bookings.push(item)
      },editItem(index){
          this.$refs.booking_model.openDialog(true,this.bookings[index],index)
      },doEditItem(details,index){
          console.log("lol")
          console.log(index)
          console.log(details)
            this.$delete(this.bookings, index)
            this.bookings.splice(index, 0, details);
      },deleteItem(index){
          this.$delete(this.bookings, index)
      }
  }
}
</script>

<style>

.booking-card{
    margin-top: 10px;
}
</style>