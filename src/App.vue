<template>
  <div class="bg-gray-200 h-screen p-4">
    <section class="top flex justify-between">
      <h1>Sorting Training System</h1>
      <button @click="handleStart" class="start-btn bg-orange-400 px-4 py-2 rounded">Start sorting!</button>
    </section>

    <div v-if="isTime">Time: {{time}}</div>
    
    <Modal @confirm-sorting="handleConfirm" @cancel-sorting="handleCancel" v-if="showModal"></Modal>
    <!-- <drag></drag> -->
    <Table v-if="showTable" :peoples="peoples"></Table>
    <!-- <dragg></dragg> -->
    
  </div>
</template>

<script>
import fakeData from '../fake_data';
import drag from './components/drag.vue';
import Modal from './components/Modal.vue';
import Table from './components/Table.vue';



  export default {
    components: {
      Modal,
      Table,
      drag,
    },
    data() {
      return {
        showModal: false,
        showTable: false,
        isTime: false,
        time: '',
        numberOfPeople: "",
        peoples: [
          // {
          //   id: 101,
          //   email: "abc@gmail.com",
          //   potatoes: 10,
          //   tags: ['Customers', 'Vip'],
          //   fullName: 'Jonab ABC',
          //   location: 'Bangladesh',
          //   date: '15/05/2022'
          // },
          // {
          //   id: 102,
          //   email: "xyz@gmail.com",
          //   potatoes: 10,
          //   tags: ['Customers'],
          //   fullName: 'Jonab XYZ',
          //   location: 'Bangladesh',
          //   date: '15/05/2022'
          // },
        ]
      }
    },
    methods: {
      handleStart() {

        this.showModal = true;
        this.showTable = false;
      },
      handleConfirm($event) {

        this.timeCountStart();
        this.isTime = true;

        this.numberOfPeople = $event;
        const data = fakeData.slice(0, $event);
        this.peoples = data;

        this.showModal = false;
        this.showTable = true;
        
        
      },
      handleCancel() {

        console.log('cancel button clicked');
        this.showModal = false;
      },

      timeCountStart() {

        let countDown = 0;
        let now = 0;
        const startTime = setInterval(() => {

          now++;
          const distance = countDown + now;
          const hours = Math.floor(distance / 3600);
          const minutes = Math.floor((distance % 3600) / 60);
          const seconds = distance % 60

          this.time = `${hours}-${minutes}-${seconds}`;
        }, 1000)
      }
    },
    
  }
</script>

<style lang="scss" scoped>

</style>