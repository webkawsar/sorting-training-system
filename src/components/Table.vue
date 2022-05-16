<template>
  <div class="bg-white p-10">
    <table class="table-auto">
      <thead>
        <tr>
          <th colspan="6" class="text-right p-4">
            {{ peoples.length }} people in the list
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
import draggable from "vuedraggable";
export default {
  props: ["peoples"],
  components: {
    draggable,
  },
  data() {
    return {
      drag: true,
    };
  },
  methods: {
    dragEnd() {
      
      let sorted = false;
      const length = this.peoples.length;
      const arr = this.peoples;

      for (let i = 0; i < length; i++) {
        const isLast = i + 1 === length;

        if (!isLast) {
          if (arr[i].potatoes < arr[i + 1].potatoes) {
            sorted = true;
          } else {
            sorted = false;
            break;
          }
        } else if (isLast) {
          if (arr[i].potatoes > arr[i - 1].potatoes) {
            sorted = true;
          }
        } else {
          sorted = false;
          break;
        }
      }

      console.log(sorted, "sorted");
      if(sorted){
        this.$emit('finished-sorting')
      }
    },
  },
  
};
</script>

<style scoped>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid gray;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
