<script setup>
import { ref, computed } from "vue";
const headerTitle = ref("Shopping List");
const items = ref([]);

const inputValue = ref("");
const priorityValue = ref("low");

const submitFunc = () => {
  items.value.push({
    id: items.value.length + 1,
    title: inputValue.value,
    priority: priorityValue.value,
    isToggledItem: false,
  });
  inputValue.value = "";
};

const reversedItems = computed(() => {
  return [...items.value].reverse();
});

const toggleItem = (item) => {
  item.isToggledItem = !item.isToggledItem;
};
</script>

<template>
  <div class="bg-slate-100 shadow-lg p-5 rounded-lg w-[500px]">
    <h1 class="text-2xl font-semibold text-center mb-[30px]">
      {{ headerTitle }}
    </h1>

    <form @submit.prevent="submitFunc" class="mb-[30px]">
      <div class="flex items-center gap-3">
        <input
          type="text"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Add an item"
          required
          v-model="inputValue"
        />
        <select
          required
          v-model="priorityValue"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-[100px] p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        >
          <option disabled value="low">Priority</option>
          <option value="low">Low</option>
          <option value="high">High</option>
        </select>
      </div>
      <button
        title="Please fill all the required fields"
        v-bind:disabled="inputValue.length === 0"
        type="submit"
        class="disabled:bg-gray-300 w-full bg-indigo-600 text-white p-2 my-3 rounded-md"
      >
        Add an item
      </button>
    </form>

    <div>
      <div v-for="item in reversedItems" :key="item.id">
        <div
          @click="toggleItem(item)"
          :class="{
            'border-l-red-400': item.priority === 'high',
            'border-l-green-400': item.priority === 'low',
            'line-through text-gray-400 border-l-gray-400':
              item.isToggledItem === true,
          }"
          class="p-2 rounded-lg bg-white my-2 border-l-[16px] hover:shadow-md duration-200 cursor-pointer"
        >
          {{ item.title }}
        </div>
      </div>
      <p v-if="!items.length" class="text-xl text-red-400">
        No added lists here
      </p>
    </div>
  </div>

  <p class="text-center text-sm text-gray-400 mt-5">
    Made with sabr, k_abdullah
  </p>
</template>

<style scoped></style>
