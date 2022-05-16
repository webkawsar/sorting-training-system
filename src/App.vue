<template>
  <div class="bg-gray-200 h-screen p-4">
    <section class="top flex justify-between">
      <h1>Sorting Training System</h1>
      <button @click="handleStart" class="start-btn bg-orange-400 px-4 py-2 rounded">Start sorting!</button>
    </section>

    <div v-if="isTime">Time: {{time}}</div>
    
    <Modal @confirm-sorting="handleConfirm" @cancel-sorting="handleCancel" v-if="showModal"></Modal>
    <!-- <drag></drag> -->
    <Table v-if="showTable" @finished-sorting="handleFinish" :peoples="peoples"></Table>
    <!-- <dragg></dragg> -->
    
  </div>
</template>

<script>
import fakeData from '../fake_data';
import Modal from './components/Modal.vue';
import Table from './components/Table.vue';



  export default {
    components: {
      Modal,
      Table,
    },
    data() {
      return {
        showModal: false,
        showTable: false,
        isTime: false,
        time: '',
        numberOfPeople: "",
        peoples: [],
        startInterval: ''
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
        this.startInterval = setInterval(() => {

          now++;
          const distance = countDown + now;
          const hours = Math.floor(distance / 3600);
          const minutes = Math.floor((distance % 3600) / 60);
          const seconds = distance % 60

          this.time = `${hours}h-${minutes}m-${seconds}s`;
          
        }, 1000);

      },
      handleFinish(){
        
        clearInterval(this.startInterval);
        this.time = ``;
        this.isTime = false;
        this.showTable = false;
        this.peoples = [];
        alert(`Congratulations!.You have use time: ${this.time}`)
      }
    },
    
  }
</script>

<style lang="scss" scoped>

</style>