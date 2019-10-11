<template>
  <b-container >
      <b-button class="booking-card" size="lg" :variant="colored?'success':''">Add new booking</b-button>
      <book-card v-for="(booking,index) in bookings" :key="index" class="booking-card"
                :description="booking.description" :booking-date="booking.date"
                :customer-name="booking.customerName"
      />
  </b-container>
</template>

<script>
import BookCard from './BookCard.vue'
export default {
    props:{
        colored:{default:true}
    },
  components: {
    BookCard
  },data(){
      return{
          bookings:[
              {date:"2019-11-19",description:"a couple with a one child",customerName:"Zammel"},
              {date:"2019-11-19",description:"a couple with a one child",customerName:"Zammel"},
          ]
      }
  }
}
</script>

<style>

.booking-card{
    margin-top: 10px;
}
</style>