<template>
  <b-container >
      <booking-dialog v-on:add-booking="addItem" v-on:edit-booking="doEditItem" ref="booking_model"></booking-dialog>
      <b-button @click="openDialog" class="booking-card" size="lg" :variant="colored?'success':''">Add new booking</b-button>
      <book-card v-for="(booking,index) in bookings" :key="index" class="booking-card"
                :description="booking.description" :booking-date="booking.date"
                :customer-name="booking.customerName"
                v-on:edit="editItem(index)"
      />
  </b-container>
</template>

<script>
import BookCard from './BookCard.vue'
import BookingDialog from './BookingDialog.vue'
export default {
    props:{
        colored:{default:true}
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
          this.bookings[index]=details;
      }
  }
}
</script>

<style>

.booking-card{
    margin-top: 10px;
}
</style>