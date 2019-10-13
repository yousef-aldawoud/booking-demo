<template>
  <b-container >
      <div v-if="!set">
          <b-button variant="success" @click="setConf(true)">Color</b-button>
          <br>
          <b-button @click="setConf(false)">No color</b-button>
          <br>
          <b-button @click="setConf(true,true)">rand color</b-button>
      </div>
      <div v-else>

      <booking-dialog v-on:add-booking="addItem" v-on:edit-booking="doEditItem" ref="booking_model" :colored="colored" :random-color="randomColor" ></booking-dialog>
      <b-button @click="openDialog" class="booking-card" size="lg" v-if="!randomColor" :variant="colored?'success':''">Add new booking</b-button>
      <b-button @click="openDialog" class="booking-card" size="lg" v-else :variant="colored?'danger':''">Adds new booking</b-button>
    <b-alert v-if="bookings.length ===0" show :variant="colored?warning:''">There are no bookings to list</b-alert>
      <book-card v-for="(booking,index) in bookings" :key="index" class="booking-card"
      :random-color="randomColor"
                :colored="colored"
                :description="booking.description" :booking-date="booking.date"
                :customer-name="booking.customerName" v-on:delete-booking="deleteItem(index)"
                v-on:edit="editItem(index)"
      />
      </div>
  </b-container>
</template>

<script>
import BookCard from './BookCard.vue'
import BookingDialog from './BookingDialog.vue'
export default {
    props:{

    },
  components: {
    BookCard,BookingDialog
  },data(){
      return{
          randomColor:false,
          success:this.randomColor ? "warning":"success",
          warning:this.randomColor ? "success":"warning",
          danger:this.randomColor ? "primary":"danger",
          primary:this.randomColor ? "danger":"primary",
          set:false,
          colored:false,
          bookings:[
          ]
      }
  },methods:{
      setConf(colored,rand=false){
          this.colored = colored;
          this.set = true;
          this.randomColor = rand
      },
      openDialog(){
          this.$refs.booking_model.openDialog();    
      },addItem(item){
          this.bookings.push(item)
      },editItem(index){
          this.$refs.booking_model.openDialog(true,this.bookings[index],index)
      },doEditItem(details,index){
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