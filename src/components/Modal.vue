<template>
    <div class="bg-white p-4 w-2/4 mx-auto">
        <div class="modal-header flex justify-between mb-4">
            <h2 class="font-bold">How many people?</h2>
            <div class="close">
                &times;
            </div>
        </div>
        <hr>
        <div class="modal-body px-2 py-6">
            <p>
                Enter a number of how many people you want to add to the list.
            </p>

            <p v-if="errors.length" class="text-red-500 font-semibold">
                {{errors[0].message}}
            </p>

            <form @submit.prevent="handleSubmit">
                <input v-model="peopleNumber" type="number" class="w-full border-2 border-slate-500 focus:outline-none px-2 py-1" name="peopleNumber rounded" id="peopleNumber">
            </form>
        </div>
        <hr>
        <div class="modal-footer text-right mt-4">
            <button @click="handleCancel" class="cancel-btn bg-gray-200 mr-2 px-4 py-1 rounded">Cancel</button>
            <button @click="handleSubmit" class="confirm-btn bg-orange-400 px-4 py-1 rounded">Start</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                errors: [],
                peopleNumber: 20
            }
        },
        methods: {
            handleSubmit(){
                if(this.peopleNumber < 20 || this.peopleNumber > 100){
                    this.errors.push({success:false, message: 'Please select number of people between 20 to 100'})
                    return false;
                }

                this.$emit('confirm-sorting', this.peopleNumber)
                return true;
            },
            // handleConfirm() {
            //     this.$emit('confirm-sorting', this.peopleNumber)
            // },
            handleCancel() {
                this.$emit('cancel-sorting')
            },
        },
    }
</script>

<style lang="scss" scoped>

</style>