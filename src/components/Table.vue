<template>
  <div class="bg-white p-10">
    
    <table class="table-auto">
        
      <thead>
        <tr>
            
            <th colspan="6" class="text-right p-4">
                {{peoples.length}} people in the list 
            </th>
        </tr>
        <tr>
          <th>Email</th>
          <th>Potatoes</th>
          <th>Tags</th>
          <th>Full name</th>
          <th>Location</th>
          <th>Date</th>
        </tr>
      </thead>

      <tbody>
        <!-- <draggable 
          v-model="peoples" 
          group="people" 
          @start="drag=true" 
          @end="drag=false" 
          item-key="id">
          <template #item="{element}">
            <tr>
              <td >{{ element.email }}</td>
              <td>{{ element.potatoes }}</td>
              <td>{{ element.tags }}</td>
              <td>{{ element.fullName }}</td>
              <td>{{ element.location }}</td>
              <td>{{ element.date }}</td>
            </tr>
          </template>
          
        </draggable> -->

        

        <!-- <tr v-for="people in peoples">
          <td>{{people.email}}</td>
          <td>{{people.potatoes}}</td>
          <td>
              <template v-for="tag in people.tags">
                  {{tag}}
              </template>
          </td>
          <td>{{people.fullName}}</td>
          <td>{{people.location}}</td>
          <td>{{people.date}}</td>
        </tr> -->
      </tbody>
      <draggable v-model="peoples" tag="tbody" item-key="name" @end="dragEnd">
          <template #item="{ element }">
            <tr style="cursor: move">
              <td scope="row">{{ element.email }}</td>
              <td>{{ element.potatoes }}</td>
              <td>{{ element.tags }}</td>
              <td>{{ element.fullName }}</td>
              <td>{{ element.location }}</td>
              <td>{{ element.date }}</td>
            </tr>
          </template>
        </draggable>
    </table>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
export default {
    props: ['peoples'],
    components: {
            draggable,
    },
    data() {
      return {
        drag: true,
      }
    },
    methods: {
      dragEnd() {
        

        let sorted = false;
        const length = this.peoples.length;
        const arr = this.peoples;
        // console.log(arr, 'arr');

        for (let i = 0; i < length ; i++) {

          // console.log(arr[i].potatoes, 'arr[i]');
          // console.log(arr[i+1], 'arr[i+1]');
          
              // console.log(arr[i].potatoes, 'current loop');
              // console.log(arr[i+1].potatoes, 'next loop');
              // console.log('-------------');

              // console.log(i, 'i');
              // if(i === 19){
              //   console.log(arr[i].potatoes, '19 er arr[i].potatoes');
              // }

            console.log(i, 'i');
            const isLast = (i+1) === length;

            if (arr[i].potatoes < (isLast ? arr[i].potatoes : arr[i+1].potatoes)) {
                sorted = true;
            } else {
              sorted = false;
              break;
            }
        }

        console.log(sorted, 'sorted');

      }
    },
    mounted() {
      // console.log(this.peoples, 'peoples');
    },
};
</script>

<style scoped>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid gray;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
