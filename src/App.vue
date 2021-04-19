<template>
  <div class="bg-gray-200">
    <div class="flex flex-col justify-center h-screen md:items-center">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="w-1/2 mx-auto mb-2 lg:mb-6 lg:w-1/4">
          <img class="" src="./assets/logo.webp" alt="" />
        </div>
        <div
          class="inline-block px-6 py-2 mx-auto align-middle min-w-1/3 lg:px-8"
        >
          <div>
            <label
              for="location"
              class="block text-sm font-medium text-gray-700"
              >Guruhingizni tanlang</label
            >
            <select
              v-model="selectedGroup"
              id="location"
              name="location"
              class="block w-full py-2 pl-3 pr-10 my-1 text-base border border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-blue-800 sm:text-sm"
            >
              <option
                v-for="(group, $groupIndex) in groupList"
                :key="group.name"
                :value="$groupIndex"
              >
                {{ group.name }}
              </option>
            </select>
          </div>
          <div v-if="selectedGroup !== null" class="flex flex-col">
            <div class="-my-2 sm:-mx-6 lg:-mx-8">
              <div
                class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
              >
                <div
                  class="overflow-hidden border-b border-gray-200 shadow sm:rounded-lg"
                >
                  <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-gray-100">
                      <tr>
                        <th scope="col" class="text-blue-800 theader">#</th>
                        <th scope="col" class="text-blue-800 theader">
                          Fanlar nomi
                        </th>
                        <th scope="col" class="text-blue-800 theader">
                          Kredit miqdori
                        </th>
                        <th scope="col" class="text-blue-800 theader">
                          Fandan olingan baho
                        </th>
                      </tr>
                    </thead>
                    <tbody>
                      <TableRaw
                        v-for="(group, $subjIndex) in groupList[selectedGroup]
                          .subjects"
                        :key="group.name"
                        class="bg-white"
                        :value="group"
                        :id="$subjIndex"
                        :totalCredits.sync="totalCredits"
                      />
                    </tbody>
                  </table>
                  <div
                    :class="{
                      'bg-green-600': gpa >= 2.7,
                      'bg-red-500': gpa < 2.7 && gpa > 0,
                    }"
                    class="flex items-center justify-end py-2 bg-blue-800"
                  >
                    <div class="text-white tdata">
                      Sizning GPA:
                      <span class="ml-2 text-xl font-bold">{{ gpa }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import Table from "./components/Table.vue";
import dataList from "./assets/data/groupList.json";
import TableRaw from "./components/TableRaw.vue";
export default {
  name: "App",
  components: { TableRaw },
  data() {
    return {
      totalCredits: {},
      selectedGroup: 0,
      pointTaken: 0,
      groupList: dataList,
    };
  },

  computed: {
    credit() {
      return Object.values(this.totalCredits).reduce(
        (prev, curr) => prev + curr,
        0
      );
    },
    gpa() {
      return (this.credit / 30).toFixed(2);
    },
  },
};
</script>

<style>
.theader {
  @apply px-6;
  @apply py-3;
  @apply text-xs;
  @apply font-medium;
  @apply tracking-wider;
  @apply text-left;
  @apply text-gray-500;
  @apply uppercase;
}

.tdata {
  @apply px-6;
  @apply py-4;
  @apply font-medium;
  @apply text-gray-800;
  @apply whitespace-nowrap;
}
</style>
