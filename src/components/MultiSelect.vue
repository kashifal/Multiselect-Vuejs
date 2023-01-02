<template>
  <div>
    <div class="relative max-w-xl mx-auto mt-8">
      <label class="block   text-lg font-normal py-2 text-gray-600">{{
        label
      }}</label>
      <div
        class="ring-1 cursor-pointer overflow-auto multi  px-2 py-2 text-sm w-full shadow focus:border-1 block focus:ring-1 focus:ring-red-600 flex gap-x-2 ring:outline-1 text-gray-700 focus:outline-blue-600 focus:border-red-400 focus:ring-red-600 rounded ring-gray-300"
        :class="arr.length <= 0 ? 'flex justify-between' : ''"
      >
        <p>{{ arr.length <= 0 ? "Languages" : "" }}</p>

        <p
          class="bg-blue-100 px-2 rounded-full"
          v-for="item in arr"
          :key="item.value"
          @click="deleteItem(item)"
        >
          {{ item.text }}
        </p>
        <p
          class="fa fa-angle-down absolute animate-pulse right-2 h-6 w-6 bg-blue-200 rounded-full flex items-center justify-center text-blue-600"
          @click="setDropdown()"
        ></p>
      </div>
      <div
        :class="dropdown ? 'block' : 'hidden'"
        class="w-full min-h-16 py-2 px-2 absolute shadow rounded ring-1 ring-gray-200 bg-white top-24"
      >
        <p
          class="text-sm font-light mt-1 text-gray-700 hover:bg-blue-700 px-1 py-2 rounded hover:text-white cursor-pointer transition-all"
          v-for="item in data"
          @click="setValue(item)"
          :key="item.value"
          :class="arr.includes(item) ? ' text-blue-700 font-black' : ''"
        >
          {{ item.text }}
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
const dropdown = ref(false);

export default {
  props: {
    label: String,
    data: Object,
  },
  setup(props) {
    const count = ref(0);
    const arr = ref([]);
    let selected = ref();
    let options = ref([
      {
        value: 1,
        text: "One",
      },
      {
        value: 2,
        text: "Two",
      },
      {
        value: 3,
        text: "Three",
      },
      {
        value: 4,
        text: "Four",
      },
      {
        value: 5,
        text: "Five",
      },
      {
        value: 6,
        text: "Six",
      },
      {
        value: 7,
        text: "Seven",
      },
    ]); 

    function setDropdown() {
      dropdown.value = !dropdown.value;
    }
    const setValue = (value) => {
      const num = value;
      if (arr.value.includes(num.value)) {
        arr.value.splice(arr.value.indexOf(num.value), 1);
        console.log(arr);
      } else {
      
        if(arr.value.includes(num)){
          return;
        }else{
  arr.value.push(num); 
        } 
        dropdown.value = !dropdown.value; 
      }
    };
    const deleteItem = (item) => {
      if (arr.value.includes(item)) {
        arr.value.splice(arr.value.indexOf(item), 1);
        options.value.unshift(item);
        selected.value = "";
        console.log(
          "cool",
          options.value.sort((item, index) => item.id - index)
        );
      }
    };

    // function setValue(value){
    //   selected.value = [...selected.value, value];
    //   dropdown.value = !dropdown.value;
    //
    // }
    return {
      count,
      selected,
      // changeLang,
      deleteItem,
      arr,
      options,
      setDropdown,
      dropdown,
      setValue,
    };
  },
};
</script>
<style scoped>
select {
  margin-top: 10px;
}
.option {
  position: relative;
  background: red;
  padding: 4px 16px;
  background: white;
  border: 1px solid black;
  border-radius: 20px;
  margin-left: 10px;
}
.close {
  position: absolute;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  top: -8%;
  left: -8%;
  background: purple;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
</style>
